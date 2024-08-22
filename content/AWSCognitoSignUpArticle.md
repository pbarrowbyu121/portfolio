# AWS Cognito Sign Up With Custom Confirmation

I’m working on migrating a web application from using Google’s Firebase to using AWS. AWS uses AWS Cognito to handle authentication for your web application. It has an option to allow users to use existing apps like Facebook, X (formerly known as Twitter), or Amazon to sign up for your web application.

The goal is to make a function that can be called by my backend that stores the user and their respective credentials in AWS so they can later sign in to my application. These users are stored in a “user pool”. A successful sign up request will add the user and their credentials to the user pool. However, this user remains ‘unconfirmed’ in the user pool. AWS sends a confirmation email to the user to confirm they have access to the email used to create the account. The confirmation email contains a confirmation code used by the user to allow the user to finish the sign-up process.

I already instigated a confirmation email process in my web application by only allowing a user to sign up if they are sent an access code via email by another user. (This is initially to limit users using data while my app is in beta). Their email address is already associated with the access code and only allowed to sign up if the correct access code is used. Consequently I need to find a way to surpass the AWS confirmation process out of the box. This can be done with a pre-sign-up Lambda function that is triggered by the sign-up. The function sets the user to confirmed without requiring the user to confirm.

## Steps

1. Create a user pool in AWS
2. Create a pre-signup lambda function
3. Write the function on the backend and test

<br />

### Create the user pool

Navigate to the Amazon Cognito service in AWS.

Click the “User pools” in the sidebar to view the user pools.

Click “Create user pool” button

Select the credential you want your user to use to sign up. I chose email.

Select the password policy you wish to use. I used the default.

Select the MFA policy you want. I opted to not require MFA.

Select the User account recovery options you want.

Click “Next”

Opt in or out of Self-service sign-up. I enabled self-registration so the user could input their email and password to sign up rather than using a pre-existing identity (like FB or Amazon) to sign up

Select Attribute verification and user account confirmation options

Select any other required attributes if desired. I opted for none except the email.

Click “Next”

Configure the message delivery. This is the email that Amazon SES will use to send emails to the user.

Click “Next”

Choose a descriptive name for the user pool

Opt in or out of the hosted authentication pages. I opted out because I’ll use a custom Frontend sign-in page

Select the App type. I chose Confidential type because my requests will be made from my backend, server-side. This will require a client secret. That created issues, but those will be addressed

Choose a descriptive app name

Click “Next”

Review your information and click “Create user pool”

### Create a pre-signup lambda function

This Lambda function will be triggered before the signup to automate the confirmation of the user’s email. I found this [page](https://docs.aws.amazon.com/cognito/latest/developerguide/user-pool-lambda-pre-sign-up.html#aws-lambda-triggers-pre-registration-example-2) in AWS Cognito documentation and used their suggested code (Python).

```jsx
def lambda_handler(event, context):
    # Confirm the user
    event['response']['autoConfirmUser'] = True

    # Set the email as verified if it is in the request
    if 'email' in event['request']['userAttributes']:
        event['response']['autoVerifyEmail'] = True

    # Set the phone number as verified if it is in the request
    if 'phone_number' in event['request']['userAttributes']:
        event['response']['autoVerifyPhone'] = True

    # Return to Amazon Cognito
    return event
```

They even include an example JSON you can use to create a Lambda function test.

Create the lambda function. Copy and past the suggested code into the “Code” tab of the function. Create the test using the suggested JSON object from the documentation. Test the function. The response should include the `response.autoConfirmUser` property.

### Write the function on the backend and test

On my backend I primarily used this [AWS git hub repository](https://github.com/awsdocs/aws-doc-sdk-examples/blob/main/javascriptv3/example_code/cognito-identity-provider/scenarios/cognito-developer-guide-react-example/frontend-client/src/authService.ts) as a springboard to create my endpoint and function to handle the sign-up authorization. It will be called by my frontend. Here’s my endpoint in Node JS:

```jsx
import express from 'express'
const router = express.Router()

router.post('/sign_up', (req, res) => {
  res.header('Access-Control-Allow-Origin', '*')
  const { email, password, accessCode } = req.body
  if (!email || !password || !accessCode) {
    return res.status(400).json({ error: 'Missing params' })
  }
  try {
    return signUpWithEmailAndPassword(
      email,
      password,
      accessCode
    ).then((resp: any) => res.json(resp))
  } catch (error) {
    console.log('error', error)
    res.status(500).json({ error: 'Error processing' })
  }
})
```

You can see it requires the email, the password, and the accessCode as mentioned earlier. Then I use another function, `signUpWithEmailAndPassword`. This is because I need to fetch the invitation record from DynamoDB to determine if the user was sent an access code:

```jsx
export function signUpWithEmailAndPassword(
  email: string,
  password: string,
  accessCode: string
) {
  return fetchInvitationRecord({ email, accessCode }).then(
    (validAccessCode) => {
      if (validAccessCode) {
        return signUp(email, password).then((resp) => resp)
      } else {
        throw new Error('Invalid access code or email')
      }
    }
  )
}
```

If there is in fact an access code record with the supplied access code and email matching, it calls the signup function. Here’s the version from the [AWS github repository](https://github.com/awsdocs/aws-doc-sdk-examples/blob/main/javascriptv3/example_code/cognito-identity-provider/scenarios/cognito-developer-guide-react-example/frontend-client/src/authService.ts):

```jsx
export const signUp = async (email: string, password: string) => {
  const params = {
    ClientId: config.clientId,
    Username: email,
    Password: password,
    UserAttributes: [
      {
        Name: 'email',
        Value: email,
      },
    ],
  }
  try {
    const command = new SignUpCommand(params)
    const response = await cognitoClient.send(command)
    console.log('Sign up success: ', response)
    return response
  } catch (error) {
    console.error('Error signing up: ', error)
    throw error
  }
}
```

HOWEVER, because when I created the user pool I selected “Confidential type,” my requests will require a client secret. I initially tried to use the above function as presented but got this error:

```jsx
Error signing up:  NotAuthorizedException: Client <redacted AWS_COGNITO_APP_CLIENT_ID> is configured with secret but SECRET_HASH was not received
```

An error saying that the SECRET_HASH was not provided.

I had to dig to find a solution. I found instruction in the [AWS Documentation](https://docs.aws.amazon.com/cognito/latest/developerguide/signing-up-users-in-your-app.html#cognito-user-pools-computing-secret-hash), but it only discussed how to do it in Python or Java, not Node JS. I did find [this helpful article](https://dev.to/shamsup/creating-the-secret-hash-for-aws-cognito-in-nodejs-50f7) (Thank you!) that discusses using node’s included `crypto` package and used its guidance to include the hash in my `signUp` function, changing it to look like this:

```jsx
import crypto from 'crypto'

export const signUp = async (email: string, password: string) => {
  if (!process.env.AWS_COGNITO_APP_CLIENT_SECRET) {
    throw new Error('AWS_COGNITO_APP_CLIENT_SECRET is not set in env')
  }
  const hasher = crypto.createHmac(
    'sha256',
    process.env.AWS_COGNITO_APP_CLIENT_SECRET
  )

  hasher.update(`${email}${process.env.AWS_COGNITO_APP_CLIENT_ID}`)
  const secretHash = hasher.digest('base64')
  const params = {
    ClientId: process.env.AWS_COGNITO_APP_CLIENT_ID,
    ClientSecret: '',
    Username: email,
    Password: password,
    SecretHash: secretHash,
    UserAttributes: [
      {
        Name: 'email',
        Value: email,
      },
    ],
  }
  try {
    const command = new SignUpCommand(params)
    const response = await cognitoClient.send(command)
    console.log('Sign up success: ', response)
    return response
  } catch (error) {
    console.error('Error signing up: ', error)
    throw error
  }
}
```

Note that the hash creation requires the “client secret.” This is found in the user pool in the AWS Congnito console. Click on the “App integration” tab, then clicking on the App client name. There you’ll find the client secret. Make sure this is passed into the `createHmac` function. Testing this in Postman gave me the following response:

```jsx
{
    "$metadata": {
        "httpStatusCode": 200,
        "requestId": "redacted-request-id",
        "attempts": 1,
        "totalRetryDelay": 0
    },
    "UserConfirmed": true,
    "UserSub": "redacted-user-sub"
}
```

This indicates the user was created AND confirmed in the user pool. Going to the user pool in the AWS console I can see the user and the ‘confirmed’ indicator.
