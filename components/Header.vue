<template>
  <div>
    <div class="header_border"></div>
    <div id="header" class="flex justify-between bg-blue-200 min-w-full">
      <div class="flex justify-between p-3">
        <img class="profile_pic" src="~/assets/images/profile_square.png" />
        <NuxtLink to="/" class="pl-10 pt-11 text-2xl font-bold text-gray-900"
          >Peter Barrow</NuxtLink
        >
      </div>
      <div class="flex justify-between p-3">
        <NuxtLink class="p-12" to="/about"><p>About</p></NuxtLink>
      </div>
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
.header_border {
  width: 100%;
  height: 0.5rem;
  background-color: rgb(83, 83, 253);
}
.profile_pic {
  border-radius: 50%;
  /* border: 5px; */
  margin-bottom: 1rem;
}
</style>
