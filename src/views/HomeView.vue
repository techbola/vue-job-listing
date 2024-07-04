<template>
  <Hero />
  <HomeCards />
  <JobListings :limit="3" showButton />
</template>

<script setup>
import Hero from '@/components/HeroComponent.vue'
import HomeCards from '@/components/HomeCards.vue'
import JobListings from '@/components/JobListings.vue'
</script>

<style lang="scss" scoped>

</style>