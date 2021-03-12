<template>
  <div id="projectsPage" class="flex-1 overflow-y-auto">
    <h1 class="text-2xl text-center mt-10 font-bold">Projects</h1>
    <div
      id="projectsContainer"
      class="m-16 max-w-lg grid gap-5 lg:grid-cols-3 lg:max-w-none"
    >
      <div v-for="project in newProjects" v-bind:key="project.id">
        <Project v-bind:project="project" />
      </div>
    </div>
  </div>
</template>

<script>
// import Project from './Project'
import projects from '../db.json'

export default {
  name: 'Projects',

  components: {
    // Project,
  },
  data() {
    return { projectsArr: [], newProjects: projects.projects }
  },
  methods: {
    async fetchProjects() {
      const res = await fetch('http://localhost:5000/projects')
      const data = await res.json()

      return data
    },
  },
  // async created() {
  //   this.projectsArr = await this.fetchProjects()
  //   console.log('created called')
  // },
}
</script>

<style lang="scss"></style>
