<!--
  This example requires Tailwind CSS v2.0+ 
  
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/typography'),
    ]
  }
  ```
-->
<template>
  <body>
    <div class="relative py-8 overflow-hidden bg-white lg:py-16">
      <div class="hidden lg:block lg:absolute lg:inset-y-0 lg:h-full lg:w-full">
        <div
          class="relative h-full mx-auto text-lg max-w-prose"
          aria-hidden="true"
        >
          <svg
            class="absolute transform translate-x-32 top-12 left-full"
            width="404"
            height="384"
            fill="none"
            viewBox="0 0 404 384"
          >
            <defs>
              <pattern
                id="74b3fd99-0a6f-4271-bef2-e80eeafdf357"
                x="0"
                y="0"
                width="20"
                height="20"
                patternUnits="userSpaceOnUse"
              >
                <rect
                  x="0"
                  y="0"
                  width="4"
                  height="4"
                  class="text-gray-200"
                  fill="currentColor"
                />
              </pattern>
            </defs>
            <rect
              width="404"
              height="384"
              fill="url(#74b3fd99-0a6f-4271-bef2-e80eeafdf357)"
            />
          </svg>
          <svg
            class="absolute transform -translate-x-32 -translate-y-1/2 top-1/2 right-full"
            width="404"
            height="384"
            fill="none"
            viewBox="0 0 404 384"
          >
            <defs>
              <pattern
                id="f210dbf6-a58d-4871-961e-36d5016a0f49"
                x="0"
                y="0"
                width="20"
                height="20"
                patternUnits="userSpaceOnUse"
              >
                <rect
                  x="0"
                  y="0"
                  width="4"
                  height="4"
                  class="text-gray-200"
                  fill="currentColor"
                />
              </pattern>
            </defs>
            <rect
              width="404"
              height="384"
              fill="url(#f210dbf6-a58d-4871-961e-36d5016a0f49)"
            />
          </svg>
          <svg
            class="absolute transform translate-x-32 bottom-12 left-full"
            width="404"
            height="384"
            fill="none"
            viewBox="0 0 404 384"
          >
            <defs>
              <pattern
                id="d3eb07ae-5182-43e6-857d-35c643af9034"
                x="0"
                y="0"
                width="20"
                height="20"
                patternUnits="userSpaceOnUse"
              >
                <rect
                  x="0"
                  y="0"
                  width="4"
                  height="4"
                  class="text-gray-200"
                  fill="currentColor"
                />
              </pattern>
            </defs>
            <rect
              width="404"
              height="384"
              fill="url(#d3eb07ae-5182-43e6-857d-35c643af9034)"
            />
          </svg>
        </div>
      </div>
      <div class="relative px-4 sm:px-6 lg:px-8">
        <div class="mx-auto text-base lg:text-lg max-w-prose">
          <h2
            class="text-base font-semibold tracking-wide text-center text-indigo-600 uppercase"
          >
            Article
          </h2>
          <h1>
            <span
              class="block mt-2 text-5xl font-extrabold leading-8 tracking-tight text-center text-gray-900"
            >
              Redux
            </span>
          </h1>
          <div
            class="m-auto text-sm prose text-center lg:text-base prose-indigo"
          >
            <p></p>
          </div>
        </div>
        <div
          id="state"
          class="mx-auto mt-12 prose prose-xl text-gray-500 prose-indigo"
        >
        <h2>State</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            React components need to manage and store information about a component’s current situation, called “state.” This information may include things like the current user, or whether or not a specific dropdown menu should be showing. Information stored in a component’s state can be passed to other children components via props.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Frequently a developer runs into situations where there is information that is pertinent across the whole app, and not just in a few components or a given component’s first few generations of children. Rather than pass this as a prop through all components, which may require passing it through components that don’t need the information, it’s easier to store this information in a “store” and then access it where needed. 
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Redux is a library used with React (it can be used with other frameworks) to manage the process of changing and accessing such a store. The store is never manipulated directly by components. “Reducer” functions are used to do that. Reducers are fed “actions” which dictate how the reducer is to change the state.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            To illustrate the use of a store, I’ve developed a polling app where
            users can vote on questions, including adding voting options and
            questions.
          </p>
          <img src='~assets/images/VotingApp.png' />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            On a side note, I’m using json-server to simulate a backend server to store questions and their corresponding options. The backend will store an array of questions, and the options are stored in a separate array, and tied to the corresponding questions via the question’s ID. The frontend makes GET, PUT, and POST requests to this server, then uses Redux to update the app with these questions and responses.
          </p>
        </div>
        <div
          id="install-redux"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Install Redux</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            To begin, install Redux:
          </p>
          <NuxtContent class="text-base" :document="installReduxCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            In the src folder, add a folder called “store” with an index file.
          </p>
          <h2>Create a Reducer</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            For this app, create a “pollReducer” which will manage the state of both questions, and voting options. 
          </p>
          <NuxtContent class="text-base" :document="pollReducerCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
           The reducer takes two arguments: state, and action. Note the initial state is set up with both questions and options set to an empty array. When this reducer is used elsewhere in the app, an action object will be passed with a type field. The type field dictates how to change the state. In the example above, if the action.type is ‘setQuestions’ the questions field in the store is set to the questions field passed in the actions object, while the options field in the store remains unchanged. The reducer function returns the state.
          </p>
        </div>
        <div
          id="create-store"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Create the Store</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
           Create the store using ‘createStore’, passing in the reducer. Export the store to be accessed elsewhere.
          </p>
          <NuxtContent class="text-base" :document="createStoreCode" />
          </div>
        <div
          id="create-provider"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Create the Provider</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Wrap the parts of the app that need access to this store in a Provider component. In this demonstration, the whole app needs access to the store, so I’ve created the Provider in the root index file and wrapped the App component in the Provider:
          </p>
          <NuxtContent class="text-base" :document="createProviderCode" />
        </div>
        <div
          id="put-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Accessing the Store</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This voting app has three main components: PollList (displays the list of different questions), PollItem (displays an individual question along with voting results), and AddPoll (used to add a question along with voting options for that question). The PollList needs access to the store to get the list of questions. The useSelector hook is used to do this, and the questions and options are then set to variables used elsewhere in the component:
          </p>
          <NuxtContent class="text-base" :document="accessingStoreCode" />
        </div>
        <div
          id="delete-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Changing the Store</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The PollItem component displays an individual question, handles the user voting, and handles adding a new option. The store is manipulated through the pollReducer using the useDispatch hook, here assigned to a variable called “dispatch”:
          </p>
          <NuxtContent class="text-base" :document="PollItemCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The addOptionHandler is used when an option is added to the question by the user:
          </p>
          <NuxtContent class="text-base" :document="addOptionHandlerCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This function calls “addOption” which adds the option to the backend, then fetches the options from the backend, and uses dispatch to update the store with those options by passing an action with a type field and an options field which contains the options returned from the backend.
          </p>
          <NuxtContent class="text-base" :document="voteHandlerCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The voteHandler function adds a vote to the vote-count of the selected option for a given question. It calls voteOption which changes the option object on the backend, then fetches all the options from the backend, and calls dispatch with the action object to update the store with the options fetched from the backend.
          </p>
        </div>
        <div
          id="delete-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Redux Toolkit</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            As more and more variables are added to the store, it may become quite large and harder to maintain. When updating the store the reducers in Redux need to include every variable in the store, regardless of whether or not it’s changing. It can also be repetitive to specify the action type each time the reducer is called. 
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            One solution to the above problems is a library called redux toolkit, which includes redux on installation. 
          </p>
          <NuxtContent class="text-base" :document="installReduxToolkitCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            I use the createSlice API (imported from @reduxjs/toolkit) to create “slices” of the store. It accepts an object as an argument with a name, initialState object, and reducers. 
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            I’ve elected to separate my pollReducer, which included options and questions, into separate slices. 
          </p>
          <NuxtContent class="text-base" :document="optionsSliceCode" />
          <NuxtContent class="text-base" :document="questionsSliceCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            If I had just one reducer I could create my store with createStore, just as I did before with pollReducer:
          </p>
          <NuxtContent class="text-base" :document="createStoreToolkitCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            But because I have multiple reducers, I use configureStore (imported from @reduxjs/toolkit):
          </p>
          <NuxtContent class="text-base" :document="configureStoreCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Now the App invokes these sliced reducers using dispatch:
          </p>
          <NuxtContent class="text-base" :document="appToolkitCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Just as before, the questions and options are fetched from the backend, then setQuestions and setOptions reducers change the state. The setQuestions and setOptions are used similarly in the PollItem and AddPoll components.
          </p>
          
            <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            In PollList, the state of questions and options is still accessed using useSelector:
          </p>
          <NuxtContent class="text-base" :document="accessingStoreRToolkitCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
           The double use of questions (“questions.questions”) is to access the questions field of the questions state.
          </p>
        </div>
        <div
          id="delete-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
        <h2>Conclusion</h2>
        This app is simple enough that it probably doesn’t need Redux, but it illustrates how Redux may be used to make managing information used across the app more manageable. Furthermore, Redux Toolkit may provide additional means of simplifying the use of Redux by allowing the user to partition reducers.
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const installReduxCode = await $content(
      'codeblocks/ReduxArticle/installRedux'
    ).fetch()
    const pollReducerCode = await $content(
      'codeblocks/ReduxArticle/pollReducer'
    ).fetch()
    const accessingStoreCode = await $content(
      'codeblocks/ReduxArticle/accessingStore'
    ).fetch()
    const addOptionHandlerCode = await $content(
      'codeblocks/ReduxArticle/addOptionHandler'
    ).fetch()
    const createProviderCode = await $content(
      'codeblocks/ReduxArticle/createProvider'
    ).fetch()
    const createStoreCode = await $content(
      'codeblocks/ReduxArticle/createStore'
    ).fetch()
    const PollItemCode = await $content(
      'codeblocks/ReduxArticle/PollItem'
    ).fetch()
    const voteHandlerCode = await $content(
      'codeblocks/ReduxArticle/voteHandler'
    ).fetch()
    const installReduxToolkitCode = await $content(
      'codeblocks/ReduxArticle/installReduxToolkit'
    ).fetch()
    const optionsSliceCode = await $content(
      'codeblocks/ReduxArticle/optionsSlice'
    ).fetch()
     const questionsSliceCode = await $content(
      'codeblocks/ReduxArticle/questionsSlice'
    ).fetch()
    const appToolkitCode = await $content(
      'codeblocks/ReduxArticle/appToolkit'
    ).fetch()
    const accessingStoreRToolkitCode = await $content(
      'codeblocks/ReduxArticle/accessingStoreRToolkit'
    ).fetch()
    const createStoreToolkitCode = await $content(
      'codeblocks/ReduxArticle/createStoreToolkit'
    ).fetch()

    return {
      installReduxCode,
      pollReducerCode,
      accessingStoreCode,
      addOptionHandlerCode,
      createProviderCode,
      createStoreCode,
      PollItemCode,
      voteHandlerCode,
      installReduxToolkitCode,
      optionsSliceCode,
      questionsSliceCode,
      appToolkitCode,
      accessingStoreRToolkitCode,
      createStoreToolkitCode
    }
  },
}
</script>

<style>
.experience-bullets {
  max-width: 800px;
}

hr {
  width: 70%;
}
</style>
