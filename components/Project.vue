<template>
  <div class="flex flex-col rounded-lg shadow-lg overflow-hidden bg-white">
    <!-- image div -->
    <div class="flex-shrink-0">
      <img class="h-48 w-full object-scale-down" :src="project.image" />
    </div>
    <!-- div for text level 1 -->
    <div class="flex-1 bg-white p-6 flex flex-col justify-between">
      <div class="flex-1">
        <a class="block mt-2"
          ><p class="text-xl font-semibold text-gray-900">
            {{ project.title }}
          </p>
          <p class="h-12 mt-3 text-base text-gray-500">
            {{ project.description }}
          </p>
        </a>
      </div>
      <div class="bg-gray-100 items-center">
        <!-- <div class="relative bg-gray-100 flex items-center mt-3 mb-3"> -->
        <!-- <div class="bg-gray-100"> -->
        <!-- <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8"> -->
        <!-- <div> -->
        <h2 class="ml-4 mt-4 text-gray-500 text-xs font-medium uppercase">
          Skills used
        </h2>
        <ul class="m-3 grid grid-cols-1 gap-3 sm:grid-cols-2 lg:grid-cols-2">
          <li
            class="content-center"
            v-for="skill in project.skills"
            v-bind:key="skill"
          >
            <p
              class="p-1 text-center text-sm justify-between border-t border-r border-b border-gray-200 bg-white rounded-r-md"
            >
              {{ skill }}
            </p>
          </li>
        </ul>
        <!-- </div> -->
        <!-- </div> -->
        <!-- </div> -->
        <!-- </div> -->
      </div>
    </div>

    <div><div class="flex pl-8 pb-2">Link</div></div>
  </div>
</template>

<script>
export default {
  name: 'Project',
  props: {
    project: Object,
  },
}
</script>

<style lang="scss"></style>
