<template>
  <div
    id="professional-experience"
    class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
  >
    <h2 class="text-center">Group Projects</h2>
    <div class="mt-8 text-sm lg:text-md" v-for="project in groupProjects" :key="project">
      <div class="grid grid-cols-4 font-bold">
        <div class="col-span-3 text-left text-md">
          {{ project.name }} - {{ project.location }}
        </div>
        <div class="text-right text-md">{{ project.dates }}</div>
      </div>
      <div class="prose experience-bullets">
        <ul class="ml-4 text-sm lg:text-base">
          <li v-for="bullet in project.bullets" :key="bullet">
            {{ bullet }}
          </li>
        </ul>
      </div>
    </div>
    <hr class="mx-auto mt-2 rounded" />
  </div>
</template>

<script>
import dbdata from '../db.json'

export default {
  name: 'GroupProjects',
  data() {
    return {
      groupProjects: dbdata.groupProjects,
    }
  },
}
</script>

<style>
hr {
  width: 70%;
}
</style>
