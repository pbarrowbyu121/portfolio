<template>
  <div id="header" class="flex justify-between bg-blue-200 min-w-full">
    <div class="p-8">
      <NuxtLink to="/" class="text-2xl font-bold text-gray-900"
        >Peter Barrow</NuxtLink
      >
    </div>
    <div class="flex justify-between p-8">
      <!-- <NuxtLink class="p-2" to="/projects">Projects</NuxtLink> -->
      <p class="p-2">About</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style>
#header {
  font-family: 'Merriweather';
}
</style>
