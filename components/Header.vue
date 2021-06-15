<template>
  <div>
    <div class="header_border"></div>
    <div id="header" class="flex justify-between bg-blue-200">
      <div class="flex justify-between">
        <img
          class="h-16 m-1 rounded-full lg:m-4 lg:h-36"
          src="~/assets/images/profile_square.png"
        />
        <NuxtLink
          to="/"
          class="m-auto text-lg font-bold text-gray-900 lg:text-4xl"
        >
          <div class="pl-2 lg:pl-4">
            <div class="mb-1 lg:mb-4">Peter</div>
            <div class="pl-1 mb-1 lg:pl-4">Barrow</div>
          </div></NuxtLink
        >
      </div>
      <div class="flex justify-between lg:mx-12">
        <NuxtLink class="m-auto mx-4 text-xs lg:mx-6 lg:text-base" to="/"
          ><p>Portfolio</p></NuxtLink
        >
        <NuxtLink class="m-auto mx-4 text-xs lg:mx-6 lg:text-base" to="/resume"
          ><p>Resume</p></NuxtLink
        >
        <NuxtLink class="m-auto mx-4 text-xs lg:mx-6 lg:text-base" to="/about"
          ><p>About</p></NuxtLink
        >
        <!-- <NuxtLink
          class="m-auto mx-4 text-xs lg:mx-6 lg:text-base"
          to="/fetchAPIarticle"
          ><p>Articles</p></NuxtLink
        > -->
        <ArticleDropdown class="m-auto mx-4 text-xs lg:mx-6 lg:text-base" />
      </div>
    </div>
  </div>
</template>

<script>
import ArticleDropdown from './ArticleDropdown.vue'
export default {
  name: 'Header',
  components: {
    ArticleDropdown,
  },
}
</script>

<style>
#header {
  font-family: 'Merriweather';
}
.header_border {
  width: 100%;
  height: 0.5rem;
  background-color: rgb(83, 83, 253);
}

/* .profile_pic {
  border-radius: 50%;
  width: 100%;
  height: auto
} */
</style>
