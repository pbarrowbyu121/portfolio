<template>
  <div class="relative mx-auto mt-10" style="max-width: 750px">
    <DotSquare />
    <NuxtContent class="" :document="article" />
  </div>
</template>

<script>
import DotSquare from '../../components/DotSquare.vue'
export default {
  components: {
    DotSquare,
  },
  async asyncData({ $content }) {
    const article = await $content('AWSCognitoSignUpArticle').fetch()

    return {
      article,
    }
  },
}
</script>

<style>
.nuxt-content h1,
.nuxt-content h2,
.nuxt-content h3 {
  font-weight: bold;
}
.nuxt-content h1 {
  font-size: 3rem;
  line-height: 1.2;
}
.nuxt-content h2 {
  font-size: 2.25rem;
}
.nuxt-content h3 {
  font-size: 1.75rem;
}
.nuxt-content p {
  margin-bottom: 10px;
}
.nuxt-content a {
  color: #007bff; /* Blue color */
  text-decoration: underline; /* Underline the link */
  cursor: pointer; /* Show pointer cursor */
}

.nuxt-content a:hover {
  color: #0056b3; /* Darker blue on hover */
  text-decoration: underline; /* Keep underline on hover */
}

.nuxt-content a:visited {
  color: #6f42c1; /* Purple color for visited links */
}

.nuxt-content a:active {
  color: #0056b3; /* Same as hover color for active links */
}
.nuxt-content ol,
.nuxt-content ul {
  list-style-position: inside;
}
.nuxt-content code {
  font-size: 14px;
}
/* Add any styles here */
</style>
