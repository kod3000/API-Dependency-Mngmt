<template>
  <footer>
    <div class="mx-auto max-w-3xl w-full block px-4 sm:px-6 lg:max-w-7xl lg:px-8">
      <div class="border-t border-gray-200 py-8 text-center text-sm text-gray-500 sm:text-left lg:text-right">

        <span class="block sm:inline">&copy; {{ year }}. </span>
        <span class="block sm:inline">All rights reserved.</span>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
const year = new Date().getFullYear()
</script>
