<template>
  <div class=" min-h-full">
    <Header @openSearch="openSearchBar" style="position:fixed; width: 100vw; padding-top:10px;top:0px; background-color: rgba(255,255,255,0.97)" class="     '~/assets/css/scrollbar.css',
 z-20 " />
    <SearchBar v-if="showSearchBar" @close="closeSearchBar" class="z-40 " />
    <div style="padding-top: 60px">
    </div>
    <NuxtPage />
    <Footer />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

import SearchBar from '../components/SearchBar.vue'

const showSearchBar = ref(false)

const openSearchBar = () => {
  showSearchBar.value = true
}

const closeSearchBar = () => {
  showSearchBar.value = false
}
</script>
