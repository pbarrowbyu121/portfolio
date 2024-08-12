<template>
  <div
    id="professional-experience"
    class="mx-auto mt-6 prose prose-xl text-gray-500 prose-indigo"
  >
    <h2 class="text-center">Professional Experience</h2>
    <div v-for="company in companyExp" :key="company" class="mt-8">
      <div class="mb-0 font-bold text-md lg:text-2xl">
        {{ company.name }} - {{ company.location }}
      </div>
      <div
        v-for="position in company.positions"
        :key="position"
        class="mt-4 text-sm lg:text-md"
      >
        <div class="grid grid-cols-4 font-bold">
          <div class="col-span-3 text-left">{{ position.title }}</div>
          <div class="text-right">{{ position.dates }}</div>
        </div>
        <div class="prose experience-bullets">
          <ul class="ml-4 text-sm lg:text-base list-none">
            <li v-for="bullet in position.bullets" :key="bullet">
              {{ bullet }}
            </li>
          </ul>
        </div>
      </div>
    </div>
    <hr class="mx-auto mt-2 rounded" />
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

<style>
hr {
  width: 70%;
}
</style>
