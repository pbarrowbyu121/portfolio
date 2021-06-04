<template>
  <div
    id="professional-experience"
    class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
  >
    <h2 class="text-center">Professional Experience</h2>
    <div class="mt-8" v-for="company in companyExp" :key="company">
      <div class="mb-0 text-2xl font-bold">
        {{ company.name }} - {{ company.location }}
      </div>
      <div class="mt-4" v-for="position in company.positions" :key="position">
        <div class="grid grid-cols-4 font-bold">
          <div class="col-span-3 text-left text-md">{{ position.title }}</div>
          <div class="text-right text-md">{{ position.dates }}</div>
        </div>
        <div class="prose experience-bullets">
          <ul class="ml-4">
            <li v-for="bullet in position.bullets" :key="bullet">
              {{ bullet }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import dbdata from '../db.json'

export default {
  name: 'CompanyExp',
  data() {
    return {
      companyExp: dbdata.professionalExperience,
    }
  },
}
</script>

<style lang="scss"></style>
