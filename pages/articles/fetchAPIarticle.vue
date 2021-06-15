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
              Fetch API
            </span>
          </h1>
          <div
            class="m-auto text-sm prose text-center lg:text-base prose-indigo"
          >
            <p></p>
          </div>
        </div>
        <div
          id="http-requests"
          class="mx-auto mt-12 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>HTTP requests and fetch API</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Fetch API allows the developer to make HTTP requests from browsers
            to servers. It allows the site to talk to a server and retrieve,
            create, edit, or destroy data on that server from the browser.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            To simulate backend servers, I’ve used json-server in my
            non-published apps. It’s a simple setup that allows me to focus on
            making fetch requests to the database rather than getting bogged
            down or distracted with setting up a backend. This server is hosted
            on a localhost port similar to the frontend.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            As a study of making HTTP fetch requests using fetch API, I’ve
            created a simple car-mileage app to track the miles per gallon for a
            number of cars. After my json-server is set up, going to
            localhost:5000/cars shows the data for different cars I’ve stored on
            my imitation server.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This app will require adding, editing, reading, and deleting data
            for cars, as well as adding, editing, reading, and deleting data for
            tanks of gas for those cars. This makes it a good example of a CRUD
            app (Create, Read, Update, Delete).
          </p>
        </div>
        <div
          id="get-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>GET requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The simplest type of HTTP request using the fetch API is a GET
            request (the R in CRUD for “read”). I’ve placed my GET request
            inside an action in Vuex (a separate topic). The request begins with
            the word “fetch”, specifying the url from where the information will
            be coming.
          </p>
          <NuxtContent class="text-base" :document="getCarActionCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Because javascript is a single-threaded language, it begins
            execution of a given line after the previous line of code has been
            started but not necessarily after the previous line has finished
            executing. The fetch request (“fetch(url)”) returns a promise that
            is created when it begins execution. It represents the eventual
            completion of this line of code (still seemingly instantaneous to
            our observation in most cases).
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The next line of code after the “fetch” begins with “.then” which is
            an instruction to only begin this line of code once the promise from
            the fetch is resolved. In this GET request, the .then statement
            turns the response (“res”) into json format, then logs it out to the
            console and uses a mutation to commit that response to the app’s
            state.
          </p>
          <NuxtContent class="text-base" :document="AppCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This fetch request in the “getCarsAction” is called in the App
            component when the app is loaded to the browser. You can also see
            that the similar “getTanksAction” is called.
          </p>
        </div>
        <div
          id="post-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>POST requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            A POST request is an HTTP request used to write data to the server
            (the C in CRUD for “create”). The anatomy of the POST request using
            the fetch API is similar to the GET request.
          </p>
          <NuxtContent class="text-base" :document="addCarActionCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            It begins with the word fetch, and the first argument is the url of
            the backend to which the data is being written. However, now there’s
            a second argument, an object with a “method” attribute to specify
            the type of request (POST in this case). Also included are a headers
            attribute specifying the data type, and a body attribute specifying
            what the data is that will actually be written to the server. This
            object could also have been included in the GET request with the
            method beings specified as “GET” but the fetch API defaults to GET
            when no method is specified.
          </p>
          <NuxtContent class="text-base" :document="onSubmitAddCarCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This addCarAction returns a promise and is called in the app in an
            “onSubmit” method which is called when the “ADD CAR” button is
            pushed, sending the newCarObj to be written to the server. After
            this promise is resolved, the “getCarsAction” discussed above is
            called.
          </p>
        </div>
        <div
          id="put-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>PUT requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            A PUT request is an HTTP request used to edit data already on the
            server (the U in CRUD for “update”). The anatomy of the PUT request
            using the fetch API is similar to the POST and GET requests
            discussed above.
          </p>
          <NuxtContent class="text-base" :document="editCarActionCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            It begins with the fetch statement, first argument is the url of the
            backend, and the second argument specifies the method, headers, and
            body of the updated data. The important difference with PUT requests
            is at the end of the url in the first argument of the fetch
            statement. The id of the item being edited (car or tank id) must be
            specified. Here it is passed in as part of the payload.
          </p>
          <NuxtContent
            class="text-base"
            :document="onSubmitEditCarActionCode"
          />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This “editCarAction” containing the fetch request is called in
            another (separate) “onSubmit” method in the app. Once the returned
            promise is resolved, the getCarsAction discussed above is again
            called to include the updated car info in the browser.
          </p>
        </div>
        <div
          id="delete-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>DELETE requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            A DELETE request is an HTTP request used to delete data already on
            the server (the D in CRUD for “delete”). The makeup of a DELETE
            request is similar to the other types of requests above.
          </p>
          <NuxtContent class="text-base" :document="deleteCarActionCode" />
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            The id of the item being deleted must be included in the first
            argument url. The method is specified in the second argument object
            as “DELETE”. A promise is returned.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This deleteCar action is called in the app when a delete button is
            clicked. Similar to above, once this returned promise is resolved,
            the getCarsAction is called.
          </p>
          <NuxtContent class="text-base" :document="deleteCarCode" />
        </div>
        <div
          id="external-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>External HTTP requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            I’ve also used the fetch API to make requests of external APIs
            containing data about the makes and models of cars available. These
            are similar to the GET requests described above. Here I’ve specified
            the method as GET in the second argument object as an example. These
            are called when filling out forms for new cars entered into the app.
          </p>
          <NuxtContent class="text-base" :document="externalAPICode" />
        </div>
        <div
          id="external-requests"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2>Where to place these requests</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Because my HTTP requests to my json server using the fetch API are
            used repeatedly throughout my app, I’ve elected to put them inside
            the global actions which are then imported into different parts of
            the code. Each action is called when needed (e.g. when app is
            created, when new car or tank of gas is created, etc.). The requests
            made to external servers are needed in only one spot so I’ve written
            those requests inside the components that use them.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            This keeps the code organized and easily maintained. This is inline
            with the DRY approach to coding, “Don’t repeat yourself.” Each
            request is written up once and used multiple times.
          </p>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const getCarActionCode = await $content(
      'codeblocks/getCarActionCode'
    ).fetch()
    const AppCode = await $content('codeblocks/AppCode').fetch()
    const addCarActionCode = await $content(
      'codeblocks/addCarActionCode'
    ).fetch()
    const onSubmitAddCarCode = await $content(
      'codeblocks/onSubmitAddCarCode'
    ).fetch()
    const editCarActionCode = await $content(
      'codeblocks/editCarActionCode'
    ).fetch()
    const onSubmitEditCarActionCode = await $content(
      'codeblocks/onSubmitEditCarActionCode'
    ).fetch()
    const deleteCarActionCode = await $content(
      'codeblocks/deleteCarActionCode'
    ).fetch()
    const deleteCarCode = await $content('codeblocks/deleteCarCode').fetch()
    const externalAPICode = await $content('codeblocks/externalAPICode').fetch()

    return {
      getCarActionCode,
      AppCode,
      addCarActionCode,
      onSubmitAddCarCode,
      editCarActionCode,
      onSubmitEditCarActionCode,
      deleteCarActionCode,
      deleteCarCode,
      externalAPICode,
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
