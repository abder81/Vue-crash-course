<script setup>
  import { ref } from 'vue'
  import Hero from '@/components/Hero.vue'
  import HomeCards from '@/components/HomeCards.vue'
  import JobListings from '@/components/JobListings.vue'
</script>

<template>
  <Hero />
  <HomeCards />
  <JobListings :limit="4" :showButton=true />
</template>