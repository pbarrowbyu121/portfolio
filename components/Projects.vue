<template>
  <div id="projectsPage" class="flex-1 overflow-y-auto bg-blue-50">
    <h1 class="mt-10 text-2xl font-bold text-center">Projects</h1>
    <div
      id="projectsContainer"
      class="grid max-w-lg gap-5 m-16 lg:grid-cols-3 lg:max-w-none"
    >
      <div v-for="project in newProjects" :key="project.id">
        <Project :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import dbdata from '../db.json'
import Project from './Project'

export default {
  name: 'Projects',

  components: {
    Project,
  },
  data() {
    return { projectsArr: [], newProjects: dbdata.projects }
  },
  methods: {
    // async fetchProjects() {
    //   const res = await fetch('http://localhost:5000/projects')
    //   const data = await res.json()
    //   return data
    // },
  },
}
</script>

<style lang="scss"></style>
