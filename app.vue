<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>

<script setup lang="ts">
useHead({
  htmlAttrs: {
    lang: 'en',
    class: 'h-full bg-white'
  },
  bodyAttrs: {
    class: 'h-full'
  }
})
</script>
