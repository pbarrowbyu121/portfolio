<template>
  <div class="relative inline-block text-left">
    <div>
      <button
        id="menu-button"
        type="button"
        class="inline-flex justify-center w-full"
        aria-expanded="true"
        aria-haspopup="true"
        @click="showDropDown = !showDropDown"
      >
        Articles
        <!-- Heroicon name: solid/chevron-down -->
        <svg
          class="w-5 h-5 ml-2 -mr-1"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
          fill="currentColor"
          aria-hidden="true"
        >
          <path
            fill-rule="evenodd"
            d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
            clip-rule="evenodd"
          />
        </svg>
      </button>
    </div>

    <!--
    Dropdown menu, show/hide based on menu state.

    Entering: "transition ease-out duration-100"
      From: "transform opacity-0 scale-95"
      To: "transform opacity-100 scale-100"
    Leaving: "transition ease-in duration-75"
      From: "transform opacity-100 scale-100"
      To: "transform opacity-0 scale-95"
  -->
    <div
      v-if="showDropDown"
      class="dropdown absolute right-0 w-56 mt-2 origin-top-right bg-white rounded-md shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
      role="menu"
      aria-orientation="vertical"
      aria-labelledby="menu-button"
      tabindex="-1"
    >
      <div class="py-1" role="none">
        <a
          id="menu-item-0"
          href="#"
          class="block px-4 py-2 text-sm text-gray-700"
          role="menuitem"
          tabindex="-1"
          @click="showDropDown = false"
          ><NuxtLink to="/articles/fetchAPIarticle">Fetch API</NuxtLink>
        </a>
      </div>
      <div class="py-1" role="none">
        <a
          id="menu-item-1"
          href="#"
          class="block px-4 py-2 text-sm text-gray-700"
          role="menuitem"
          tabindex="-1"
          @click="showDropDown = false"
          ><NuxtLink to="/articles/ReduxArticle">Redux</NuxtLink>
        </a>
      </div>
      <div class="py-1" role="none">
        <a
          id="menu-item-2"
          href="#"
          class="block px-4 py-2 text-sm text-gray-700"
          role="menuitem"
          tabindex="-1"
          @click="showDropDown = false"
          ><NuxtLink to="/articles/algoliaAWSintegration"
            >Algolia & AWS Layers</NuxtLink
          ></a
        >
      </div>
      <div class="py-1" role="none">
        <a
          id="menu-item-2"
          href="#"
          class="block px-4 py-2 text-sm text-gray-700"
          role="menuitem"
          tabindex="-1"
          @click="showDropDown = false"
          ><NuxtLink to="/articles/awsCognitoSignUp"
            >AWS Cognito Sign Up</NuxtLink
          ></a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ArticleDropdown',
  data() {
    return {
      showDropDown: false,
    }
  },
}
</script>

<style>
.dropdown {
  z-index: 20;
}
</style>
