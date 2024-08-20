# Integrate AlgoliaSearch with AWS DynamoDB, Lambda Functions

Algolia is a hosted search engine that provides a search experience for the user, delivering search results in real time. I recently had trouble integrating this with my AWS environment for an app that I’m working on. Here’s an article to remind future-me how I did this. Specifically, I needed to make an AWS Lambda function that was triggered by the addition of a new user to my ‘users’ table in DynamoDB that would then add a corresponding user record to my existing Algolia index.

I first tried doing this in Python (my preference for AWS Lambda functions), but kept running into problems for which I could not find adequate solutions. So I decided to do this in Node.js 20.x.

This article assumes the following:

- Active Algolia account with an existing index (this keeps the records that will be searched)
- AWS Account with appropriate permissions to write and implement a Lambda Function and DynamoDB Stream
- You’re using a MacOS (most of this should be the same for Windows)

<br />

## Steps Overview

1. Create an AWS Lambda Function Layer for Algolia
2. Configure DynamoDB Stream
3. Create an IAM Policy for the IAM Role
4. Create an IAM Role for the function
5. Create the AWS Lambda Function
6. Add the Layer to the AWS Lambda Function
7. Add a Trigger to the AWS Lambda Function

<br />

## Details

### 1. Create an AWS Lambda Function Layer for Algolia

AWS Lambda layers are a way to manage and share common code and dependencies across multiple Lambda functions. A layer is a ZIP archive that contains libraries, a custom runtime, or other dependencies.

This [guidance from AWS](https://docs.aws.amazon.com/lambda/latest/dg/packaging-layers.html) indicates what the path for a layer needs to look like. This allows Lambda functions to correctly access dependencies that are uploaded as a layer. To follow this guidance, create a directory to install `algoliasearch` (here the name of the directory doesn’t matter), and navigate into the created folder:

```jsx
mkdir algolia-layer
cd algolia-layer
```

Initiate a package.json file so you can install `algoliasearch`

```jsx
npm init -y
```

Install `algoliasearch`

```jsx
npm install algoliasearch
```

At this point I opened up this directory in VS Code to make sure I could appropriately import algoliasearch assets into a test node.js file. This is where I was running into issues with Python, trying to import algoliasearch.

Compress the newly created directory in which you installed `algoliasearch`, either by using the UI or command line. I used the UI by right clicking the folder `algolia-layer` and selecting “Compress ‘algolia-layer’”. This created a zip file, `algolia-layer.zip` This zip file will become the layer for our AWS Lambda function.

In AWS, navigate to the Lambda service, select “Layers” in the sidebar. Click the “Create Layer” button. Fill out the presented form. I named my layer “algoliasearch-nodejs-layer”. Upload the zip file. Select Node.js 20.x as the Compatible runtime (or whichever corresponds to your Node.js version).

### 2. Configure DynamoDB Stream

Navigate to the DynamoDB service UI in AWS.

Select “Tables” in the sidebar.

Select the appropriate table that we’re aiming to monitor. Mine is called ‘users’.

Make sure you’re viewing the table details, not the table items.

Select the Exports and Streams tab.

In the “DynamoDB stream details” table, click “Turn On”. This will show the “DynamoDB stream details” and “View type” options. I selected the “New image” option since I’m only interested in the new version of the changed/added user object. Click the “Turn on stream”. This should navigate back to the “Exports and Streams” tab.

Now you’ll see details for the DynamoDB Stream, including the Stream Status, View type, and Latest stream ARN. Take note of this. It will be needed to create a permission policy for your AWS Lambda function.

### 3. Create an IAM Policy

Navigate to the IAM service UI in AWS.

Click “Create Policy”.

Select the JSON option to edit your policy permissions. It needs permission to access the DynamoDB Stream created above. It will also need the ARN from your DynamoDB for the “Resource” property. Here’s what mine looks like:

```jsx
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "dynamodb:GetItem",
                "dynamodb:PutItem",
                "dynamodb:UpdateItem",
                "dynamodb:DeleteItem",
                "dynamodb:Query",
                "dynamodb:Scan",
                "dynamodb:DescribeStream",
                "dynamodb:GetRecords",
                "dynamodb:GetShardIterator",
                "dynamodb:ListStreams"
            ],
            "Resource": "arn:aws:dynamodb:<redacted region>:<redacted account #>:table/users/stream/2024-08-19T20:36:52.764"
        }
    ]
}
```

Click “Next”.

Name the function something descriptive. I named mine “Algolia-read-users-table-policy”.

Click “Create policy”

### 4. Create an IAM Role

Navigate to the IAM Service UI.

Select “Roles” in the sidebar.

Click “Create Role”.

Select “AWS Service” for “Trusted entity type”

Select Lambda for the “Use Case”

Click “Next”

For “Permissions policies” needed, select the policy created above, “Algolia-read-users-table-policy”. Also make sure the AWS Managed policy “AWSLambdaBasicExecutionRole” is selected.

Click “Next”

Name the role something descriptive and informative. Maybe include a good Description.

Click “Create role”

### 5. Create an AWS Lambda Function

Navigate to the AWS Lambda service UI. Select “Functions” in the sidebar.

Click the “Create function” button in the upper right. I opted for the “Author from scratch” options.

Name the function something descriptive. I named mine “algolia-add-users”.

Select the appropriate Runtime. Mine was Node.js 20.x

Under “Change default execution role”, select “Use an existing role”. In the dropdown select the role created above.

Click “Create function”

Click the “Configuration” tab in the function UI to add Environment Variables.

Click “Environment Variables” tab on the left sidebar.

Add `ALGOLIA_ADMIN_API_KEY`, `ALGOLIA_APP_ID`, `ALGOLIA_INDEX_NAME` and their corresponding values.

Go back to the “Code” tab

Here’s what the Code in index.mjs should look like:

```jsx
import { algoliasearch } from 'algoliasearch'

const ALGOLIA_APP_ID = process.env.ALGOLIA_APP_ID
const ALGOLIA_ADMIN_API_KEY = process.env.ALGOLIA_ADMIN_API_KEY
const ALGOLIA_INDEX_NAME = process.env.ALGOLIA_INDEX_NAME

const client = algoliasearch(ALGOLIA_APP_ID, ALGOLIA_ADMIN_API_KEY)

export const handler = async (event) => {
  const promises = event.Records.map(async (rec) => {
    if (rec.dynamodb.NewImage) {
      const newImage = rec.dynamodb.NewImage

      // Extract necessary fields
      const record = {
        uid: newImage.uid.S,
        username: newImage.username.S,
        email: newImage.email.S,
      }

      // Add record to Algolia
      try {
        await client.saveObject({ indexName: ALGOLIA_INDEX_NAME, body: record })
      } catch (error) {
        console.error(`Failed to add record with uid ${record.uid}:`, error)
      }
    }
  })

  // Await all promises to ensure all records are processed
  await Promise.all(promises)

  const response = {
    statusCode: 200,
    body: JSON.stringify('Processing Complete'),
  }
  return response
}
```

Create a Test to make sure the function works. Click the “Test” dropdown and “Configure test event”

Give it a descriptive name

We are trying to simulate an event from the DynamoDB Stream. Mine looks like this:

```jsx
{
  "Records": [
    {
      "eventID": "1",
      "eventName": "INSERT",
      "eventVersion": "1.0",
      "eventSource": "aws:dynamodb",
      "awsRegion": "us-west-2",
      "dynamodb": {
        "ApproximateCreationDateTime": 1692485599,
        "Keys": {
          "userId": {
            "S": "12345"
          }
        },
        "NewImage": {
          "uid": {
            "S": "12345"
          },
          "username": {
            "S": "John_Doe"
          },
          "email": {
            "S": "johndoe@example.com"
          }
        },
        "SequenceNumber": "111",
        "SizeBytes": 26,
        "StreamViewType": "NEW_AND_OLD_IMAGES"
      },
      "eventSourceARN": "arn:aws:dynamodb:<region redacted>:<account # redacted>:table/users/stream/2024-08-20T00:00:00.000"
    }
  ]
}
```

Don’t invoke this test yet. We need to add the Algolia layer we made earlier to this function so it can use the algoliasearch dependency

### 6. Add the Layer to the AWS Lambda Function

In the Function UI > Diagram UI, click the Layers under the function.

Click “Add a layer”

Select “Custom layers”

Select the layer created above.

Click “Add”

Now it’s time to test this function. Invoke the test and hope that the response is the successful 200. If successful you should also see the test record added in your Algolia index.

### 7. Add a Trigger to the AWS Lambda Function

In the Function UI > Diagram UI, click “+ Trigger”

Select DynamoDB as the source.

Select the appropriate table. I’m trying to monitor the ‘users’ table so I select that one.

Click “Add”

Adding this trigger now makes it so that the function runs when a new record is added to the ‘users’ table in DynamoDB.

This should sufficiently configure your lambda function to monitor your DynamoDB table. When a new record is added to the DynamoDB table, the Lambda function integrates with Algolia to add an object to the appropriate index in Algolia.
