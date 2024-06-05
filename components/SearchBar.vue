<template>
  <div v-if="show" class="fixed inset-0 overflow-y-auto">
    <div class="fixed inset-0 bg-slate-900/80 bg-gradient-to-b from-slate-900/90 to-slate-900/45"></div>
    <div class="flex min-h-full items-start justify-center p-4 text-center">
      <div
          id="headlessui-dialog-panel-15"
          data-headlessui-state="open"
          class="w-full max-w-3xl transform rounded-2xl bg-white mt-20 p-2 text-left align-middle shadow-xl transition-all"
      >
        <div class="">
          <div class="relative">
            <input
                ref="searchInput"
                type="text"
                placeholder="Search..."
                v-model="searchQuery"
                class="border-0 w-full rounded-xl bg-white py-4 pr-3 pl-12 text-gray-900 ring-2 ring-inset ring-zinc-200 focus:ring-2 focus:ring-inset focus:ring-transparent text-lg"
            />
            <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                aria-hidden="true"
                data-slot="icon"
                class="pointer-events-none absolute left-4 top-5 h-5 w-5"
            >
              <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z"
              ></path>
            </svg>
          </div>
        </div>
        <div class="" v-if="searchQuery && filteredData.length > 0 && show">
          <ul class="pt-2 max-h-[31rem] divide-y divide-slate-200 overflow-y-auto rounded-b-lg text-sm leading-6">
            <li v-for="project in filteredData" :key="project.url" class="flex items-center justify-between p-4">
              <div class="flex flex-col grow">
                <a :href="project.url" target="_blank" class="flex gap-4 bg-zinc-100 hover:bg-zinc-200 p-3 rounded-xl group focus">
                  <div class="flex shrink-0 rounded-lg overflow-hidden bg-gray-400 w-20 h-20">
                  </div>
                  <div class="flex flex-col justify-center grow">
                    <div class="flex items-center">
                      <span class="py-1 grow font-semibold group-hover">{{ project.name }}</span>
                    </div>
                    <span class="line-clamp-2">{{ project.description }}</span>
                    <div class="flex gap-2 pt-3 pb-1 flex-wrap">
                      <span v-for="(dependatnt, index) in project.dependencies" :key="index" class="text-xs px-2 py-0.5 text-slate-700 font-bold border-2 border-slate-600 rounded-full">{{ dependatnt.name }}</span>
                    </div>
                  </div>
                </a>
              </div>
            </li>
          </ul>
        </div>
        <div v-else-if="searchQuery && filteredData.length === 0" class="p-4">
          <p>No results found.</p>
        </div>
        <div class="hidden lg:flex absolute -right-14 top-4">
          <button type="button" @click="closeSearchBar" class="inline-flex justify-center rounded-md border border-transparent px-4 py-2 text-sm font-medium focus:outline-none focus-visible:ring-2  focus-visible:ring-offset-2">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon" class="h-6 w-6 z-10 text-white drop-shadow-lg">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { projects as projectData } from "~/constants/projects.ts";
const show = ref(true)
const emit = defineEmits(['close'])

const searchQuery = ref('')
const searchInput = ref(null)

const filteredData = computed(() => {
  const query = searchQuery.value.toLowerCase().trim();
  if (query === '') {
    return [];
  }
   return projectData.filter(project =>
      project.name && project.name.toLowerCase().includes(query) ||
      project.description && project.description.toLowerCase().includes(query) ||
      project.dependencies && project.dependencies.some(dependant =>
        dependant.name.toLowerCase().includes(query)
      )
  );
});

const closeSearchBar = () => {
  show.value = false
  emit('close')
}

onMounted(() => {
  searchInput.value.focus()
})
</script>
<style scoped>
.group:hover .group-hover {
  /* your desired hover styles */
}
</style>
