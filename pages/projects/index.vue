<template>
  <section style="z-index: -1" class="bg-white-600 pb-24 pt-12 -mt-12">
  </section>
  <main class="mt-24   lg:pt-0">

    <div class="bg-white" v-if="project">
      <div class="mx-auto max-w-7xl px-6  lg:px-8 ">
        <div class="card-container" :class="{ 'flip': !lockProjectDetails }">
          <div class="card-front">
            <div class="lg:grid lg:grid-cols-12 lg:gap-8">
              <div class="lg:col-span-5">
                <h2 class="text-2xl font-bold leading-10 tracking-tight text-gray-900">{{ project.name }}</h2>
                <p class="mt-4 text-base leading-7 text-gray-600">{{ project.description }}</p>
                <button @click="lockProjectDetails = false">Edit</button>
              </div>
              <div class="mt-10 lg:col-span-7 lg:mt-0">
                <dl class="space-y-10">
                  <div v-for="(dependency, index) in project.dependencies" :key="index">
                    <dt class="text-base font-semibold leading-7 text-gray-900">{{ dependency.name }} - {{ dependency.status }}</dt>
                    <dd class="mt-2 text-base leading-7 text-gray-600"></dd>
                  </div>
                </dl>
              </div>
            </div>
          </div>
          <div class="card-back">
            <form @submit.prevent="saveProject">
              <div class="lg:grid lg:grid-cols-12 lg:gap-8">
                <div class="lg:col-span-5">
                  <div class="sm:col-span-4">
                    <label for="username" class="block text-sm font-medium leading-6 text-gray-900">Project Name</label>
                    <div class="mt-2">
                      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                        <input type="text"   v-model="project.name"  name="projectname" id="projectname" class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" placeholder="janesmith" />
                      </div>
                    </div>
                  </div>

                  <div class="col-span-full mt-3">
                    <label for="about" class="block text-sm font-medium leading-6 text-gray-900">Description</label>
                    <div class="mt-2">
                      <textarea id="description" v-model="project.description" name="description" rows="3" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                    </div>
                    <p class="mt-1 text-sm leading-6 text-gray-600">Write a few sentences about the project.</p>
                  </div>
                  <div class="sm:col-span-4 mt-3">
                    <label for="username" class="block text-sm font-medium leading-6 text-gray-900">Project Url</label>
                    <div class="mt-2">
                      <div class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md">
                        <input type="text" v-model="project.url"  name="projecturl" id="projecturl"  class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6" placeholder="janesmith" />
                      </div>
                    </div>
                  </div>
                  <div class="mt-6 flex items-center justify-end gap-x-6">
                    <button @click="lockProjectDetails = true" type="button" class="text-sm font-semibold leading-6 text-gray-900">Cancel</button>
                    <button type="submit" class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Save</button>
                  </div>
                </div>
                <div class=" boom mt-10 lg:col-span-7 lg:mt-0">
                  <h3 class="text-lg font-semibold leading-6 text-gray-900">Dependencies</h3>
                  <dl class="space-y-10">
                    <div v-for="(dependency, index) in project.dependencies" :key="index">

                      <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
                      <div class="sm:col-span-3">
                        <label for="first-name" class="block text-sm font-medium leading-6 text-gray-900">Name</label>
                        <div class="mt-2">
                          <input type="text" v-model="dependency.name" name="dependantName" id="dependantName"   class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                        </div>
                      </div>

                      <div class="sm:col-span-3">
                        <label for="last-name" class="block text-sm font-medium leading-6 text-gray-900">URL</label>
                        <div class="mt-2">
                          <input type="text" v-model="dependency.url" name="depandantUrl" id="depandantUrl"  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                        </div>
                      </div>
                      </div>

                    </div>
                    <div>
                      <button type="button"  @click="addDependency" class="rounded-md bg-white px-2.5 py-1.5 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50">Add Dependency</button>
                    </div>
                  </dl>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <div class="bg-white" v-else>
      <div class="mx-auto max-w-7xl px-6 py-24 lg:px-8 lg:py-40">
        <div class="lg:grid lg:grid-cols-12 lg:gap-8">
          <div class="lg:col-span-5">
            <h2 class="text-2xl font-bold leading-10 tracking-tight text-gray-900">Project Not Found</h2>
            <p class="mt-4 text-base leading-7 text-gray-600">The project you're looking for doesn't exist</p>
          </div>
          <div class="mt-10 lg:col-span-7 lg:mt-0">
            <dl class="space-y-10">
            </dl>
          </div>
        </div>
      </div>
    </div>

  </main>
</template>

<script setup lang="ts">
import { projects } from '~/constants/projects.ts';
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import axios from 'axios';

const route = useRoute();
const projectId = route.query.id as string;
const project = ref(projects.find((p) => p.id === parseInt(projectId)));
const lockProjectDetails = ref(true);
const saveProject = () => {

  // save changes to the project, name description and url
  if (project.value.name === '' || project.value.description === '' || project.value.url === '') {
    lockProjectDetails.value = true;

    return;
  }
  if (project.value.dependencies[project.value.dependencies.length - 1].name === '' || project.value.dependencies[project.value.dependencies.length - 1].url === '') {
    lockProjectDetails.value = true;

    return;
  }

  lockProjectDetails.value = true;
};

const addDependency = () => {

  if (project.value.dependencies[project.value.dependencies.length - 1].name === '' || project.value.dependencies[project.value.dependencies.length - 1].url === '') {
    return;
  }
  project.value.dependencies.push({
    name: '',
    url: '',
    status: 'ok',
  });
};


onMounted(() => {
  if (project.value) {


  }
});
</script>

<style scoped>
.card-container {
  position: relative;
  height: max-content;
  transform-style: preserve-3d;
  transition: transform 0.5s;
  min-height: 50vh;
  height: auto;
  max-height: 50vh;
  margin-bottom: 10vh;
}

.card-front,
.card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow:hidden;

  backface-visibility: hidden;
}
.boom{
  overflow-y: auto;
  max-height: 50vh;
}
.card-back {
  transform: rotateY(180deg);
}

.flip {
  transform: rotateY(180deg);
}
</style>
