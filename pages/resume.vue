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
          <h1>
            <span
              class="block mt-2 text-4xl font-extrabold leading-8 tracking-tight text-center text-gray-900"
            >
              Peter A Barrow
            </span>
          </h1>
          <div
            class="m-auto text-sm prose text-center lg:text-base prose-indigo"
          >
            <p>
              <a href="https://www.gmail.com" target="_blank"
                >pbarrowbyu@gmail.com</a
              >
              |
              <a href="https://github.com/pbarrowbyu121" target="_blank"
                >github.com/pbarrowbyu121</a
              >
              |
              <a href="https://www.linkedin.com/in/pbarrowbyu/" target="_blank"
                >LinkedIn</a
              >
            </p>
          </div>
        </div>
        <div
          id="summary"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2 class="text-center">Summary</h2>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            I am a self-taught frontend web developer who transitioned from a
            career in actuarial science in 2020 to pursue my passion for coding.
            I acquired my skills through platforms like FreeCodeCamp.org,
            Frontend Masters, and YouTube, driven by my enjoyment of
            problem-solving and the creative challenges of web development. I
            have applied my knowledge by creating a personal website that
            simulates stock trading, demonstrating my ability to innovate and
            apply technical skills in practical projects.
          </p>
          <p class="mt-4 text-base leading-8 text-gray-500 lg:text-xl">
            Technical skills: HTML/HTML5, CSS, Javascript/JS, Vue/Vuex, Quasar,
            React/Redux, TypeScript, Tailwind, Bootstrap, Chrome dev tools
          </p>
          <hr class="mx-auto mt-2 rounded" />
        </div>

        <CompanyExp />
        <GroupProjects />
        <div
          id="certications"
          class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
        >
          <h2 class="text-center">Certifications</h2>
          <div class="mt-8">
            <div class="mb-0 font-bold text-md lg:text-2xl">
              Bachelors of Science in Mathematics
            </div>
            <div class="text-sm font-bold lg:text-md">
              Brigham Young University
            </div>
            <div class="text-xs lg:text-base">
              Other courses taken: Accounting, Economics, Statistics, Computer
              Science
            </div>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
import CompanyExp from '../components/CompanyExp.vue'
import GroupProjects from '../components/GroupProjects.vue'

export default {
  components: {
    CompanyExp,
    GroupProjects,
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
