<template>
  <div class="profile-page">
    <NuxtPage />
  </div>
</template>

<script setup lang="ts">
/*
 * app.vue is loaded only once
 **/
import { useImagesStore } from '@/stores/images'
const imageStore = useImagesStore()

onBeforeMount(() => {
  console.log('Project images: ', import.meta.glob('@/assets/projects/*.png', { eager: true }))
  imageStore.setImages(import.meta.glob('@/assets/projects/*.png', { eager: true }))
})
</script>
