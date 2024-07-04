<template>
  <section class="bg-green-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" class="bg-white rounded-xl shadow-md relative" />
      </div>
    </div>
  </section>

  <section v-if="state.jobs.length > 0 && showButton" class="m-auto max-w-lg my-10 px-6">
    <router-link
      :to="{ name: 'Jobs' }"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >
      View All Jobs
    </router-link>
  </section>
</template>

<script setup>
import { reactive, onMounted } from 'vue';
import JobListing from '@/components/JobListing.vue';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import axios from 'axios';

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false
  }
});

const state = reactive({
  jobs: [],
  isLoading: false
});

onMounted(async () => {
  try {
    state.isLoading = true
    const { data } = await axios.get('http://localhost:8000/jobs');
    state.jobs = data
  } catch (error) {
    console.error('Error fetching jobs', error)
  } finally {
    state.isLoading = false
  }
})
</script>

<style lang="scss" scoped>

</style>