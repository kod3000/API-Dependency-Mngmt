<template>
  <main class="mt-24 pb-8 lg:pt-0 pt-64">
    <div class="bg-white  ">
      <div class="mx-auto max-w-7xl px-6 lg:px-8">
        <div class="mx-auto max-w-2xl lg:mx-0">
          <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">Projects</h2>
          <p class="mt-2 text-lg leading-8 text-gray-600">Here we have a list of projects</p>
        </div>
        <div class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-x-8 gap-y-16 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
          <article v-for="project in projects" :key="project.id" class="flex max-w-xl p-3 border flex-col items-start justify-start">

            <div class="group relative">
              <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600">
                <nuxt-link :to="{ path: '/projects', query: { id: project.id } }">
                  <span class="absolute inset-0" />
                  {{ project.name }}
                </nuxt-link>
              </h3>
              <p class="mt-5 line-clamp-3 text-sm leading-6 text-gray-600">{{ project.description }}</p>
            </div>
            <p class="mt-2 text-sm font-semibold leading-8 text-gray-600">Dependencies :</p>

            <div class="flow-root">
              <ul role="list" class="-mb-8">
                <li v-for="(dependancy, dependancyIdx) in project.dependencies" :key="dependancy.id">
                  <div class="relative pb-8">
                    <span v-if="dependancyIdx !== project.dependencies.length - 1" class="absolute left-4 top-4 -ml-px h-full w-0.5 bg-gray-200" aria-hidden="true" />
                    <div class="relative flex space-x-3">
                      <div>
              <span :class="[dependancy.iconBackground, 'h-8 w-8 rounded-full flex items-center justify-center ring-8 ring-white']">
                <component :is="dependancy.icon" class="h-5 w-5 text-white" aria-hidden="true" />
              </span>
                      </div>
                      <div class="flex min-w-0 flex-1 justify-between space-x-4 pt-1.5">
                        <div>
                          <p class="text-sm text-gray-500">
                            {{ dependancy.name }} - {{ dependancy.status }}
                          </p>
                        </div>
                        <div class="whitespace-nowrap text-right text-sm text-gray-500">
                          <time :datetime="dependancy.datetime">{{ dependancy.date }}</time>
                        </div>
                      </div>
                    </div>
                  </div>
                </li>
              </ul>
            </div>
          </article>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { projects } from "../constants/projects.ts";
import { CheckIcon, HandThumbUpIcon, UserIcon } from '@heroicons/vue/20/solid';

// Declare the data properties
const data = {
  projects: projects
};
</script>
