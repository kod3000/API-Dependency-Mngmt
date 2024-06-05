<template>
  <Popover as="header" class="bg-white-600 z-20  " v-slot="{ open }"   >
    <div class="mx-auto max-w-3xl px-4 sm:px-6 lg:max-w-7xl lg:px-8">
      <div class="relative flex items-center justify-center lg:justify-between">
        <!-- Logo -->
        <div class="inline-flex w-full  justify-between min-h-12 pb-2">

        <div class="absolute left-0 flex-shrink-0 lg:static">
          <a href="/">
            <span class="sr-only">Dependancies</span>
          </a>
        </div>
          <nav class="hidden space-x-4  lg:block">
            <a v-for="item in externalLinks" :key="item.name" :href="item.href" target="_blank" :class="[item.current ? 'text-green' : 'text-green-100', 'rounded-md bg-white bg-opacity-0 px-3 py-2 text-sm font-medium hover:bg-opacity-10']" :aria-current="item.current ? 'page' : undefined">
             <span class="inline-flex x-2" >
               <span class="mr-1" >
               {{ item.name }}
               </span>
               <span>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="size-4">
                <path d="M6.22 8.72a.75.75 0 0 0 1.06 1.06l5.22-5.22v1.69a.75.75 0 0 0 1.5 0v-3.5a.75.75 0 0 0-.75-.75h-3.5a.75.75 0 0 0 0 1.5h1.69L6.22 8.72Z" />
                <path d="M3.5 6.75c0-.69.56-1.25 1.25-1.25H7A.75.75 0 0 0 7 4H4.75A2.75 2.75 0 0 0 2 6.75v4.5A2.75 2.75 0 0 0 4.75 14h4.5A2.75 2.75 0 0 0 12 11.25V9a.75.75 0 0 0-1.5 0v2.25c0 .69-.56 1.25-1.25 1.25h-4.5c-.69 0-1.25-.56-1.25-1.25v-4.5Z" />
              </svg>
               </span>
             </span>
            </a>
          </nav>
        </div>

        <!-- Menu button -->

        <div class="absolute right-0 flex-shrink-0 lg:hidden">
          <!-- Mobile menu button -->
          <PopoverButton class="relative inline-flex items-center justify-center rounded-md bg-transparent p-2 text-green-800 hover:bg-white hover:bg-opacity-10 hover:text-green focus:outline-none focus:ring-2 focus:ring-white">
            <span class="absolute -inset-0.5" />
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </PopoverButton>
        </div>
      </div>
      <div class="hidden border-t border-white border-opacity-20 py-5 lg:block">
        <div class="grid grid-cols-3 items-center gap-8">
          <div class="col-span-2">
            <nav class="flex space-x-4">
              <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current ? 'text-green' : 'text-green-800', 'rounded-md bg-white bg-opacity-0 px-3 py-2 text-sm font-medium hover:bg-opacity-10']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</a>
            </nav>
          </div>
          <div>
            <div class="mx-auto w-full max-w-md">
              <label for="mobile-search" class="sr-only">Search</label>
              <div class="relative text-green focus-within:text-green-600">
                <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3">
                  <MagnifyingGlassIcon class="h-5 w-5" aria-hidden="true" />
                </div>
                <input id="mobile-search"
                       autocomplete="off"
                       @focus="openSearchComponent"
                       class="block w-full rounded-md border-0 bg-white/20 py-1.5 pl-10 pr-3 text-green placeholder:text-green focus:bg-white focus:text-green-900 focus:ring-0 focus:placeholder:text-green-500 sm:text-sm sm:leading-6" placeholder="Search" type="search" name="search" />
              </div>
            </div>
          </div>
        </div>


      </div>

    </div>

    <TransitionRoot as="template" :show="open">
      <div class="lg:hidden">
        <TransitionChild as="template" enter="duration-150 ease-out" enter-from="opacity-0" enter-to="opacity-100" leave="duration-150 ease-in" leave-from="opacity-100" leave-to="opacity-0">
          <PopoverOverlay class="fixed inset-0 z-20 bg-black bg-opacity-25" />
        </TransitionChild>

        <TransitionChild as="template" enter="duration-150 ease-out" enter-from="opacity-0 scale-95" enter-to="opacity-100 scale-100" leave="duration-150 ease-in" leave-from="opacity-100 scale-100" leave-to="opacity-0 scale-95">
          <PopoverPanel focus class="absolute inset-x-0 top-0 z-30 mx-auto w-full max-w-3xl origin-top transform p-2 transition">
            <div class="divide-y divide-green-800 rounded-lg bg-white shadow-lg ring-1 ring-black ring-opacity-5">
              <div class="pb-2 pt-3">
                <div class="flex items-center justify-between px-4">

                  <div class="-mr-2">
                    <PopoverButton class="relative inline-flex items-center justify-center rounded-md bg-white p-2 text-green-400 hover:bg-green-100 hover:text-green-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white-500">
                      <span class="absolute -inset-0.5" />
                      <span class="sr-only">Close menu</span>
                      <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                    </PopoverButton>
                  </div>
                </div>
                <div class="mt-3 space-y-1 px-2">
                  <a v-for="item in navigation" :key="item.name" :href="item.href" :class="['block rounded-md px-3 py-2 text-base font-medium text-green-900 hover:bg-green-100 hover:text-green-800']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</a>
                </div>
              </div>
            </div>
          </PopoverPanel>
        </TransitionChild>
      </div>
    </TransitionRoot>
  </Popover>
</template>

<script setup lang="ts">
import {
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  Popover,
  PopoverButton,
  PopoverOverlay,
  PopoverPanel,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'
import { Bars3Icon, BellIcon, XMarkIcon } from '@heroicons/vue/24/outline'
import { MagnifyingGlassIcon } from '@heroicons/vue/20/solid'
import {SearchBar} from "#components";


const navigation = [
  { name: 'Home', href: '/', current: false }
]

const externalLinks = [
  ]

const emit = defineEmits(['openSearch'])

const openSearchComponent = () => {
  emit('openSearch')
}

</script>
