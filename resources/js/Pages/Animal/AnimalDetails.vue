<script setup>
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
import { Head } from '@inertiajs/inertia-vue3';
import { Inertia } from "@inertiajs/inertia";
import { Link } from '@inertiajs/inertia-vue3';
import { useForm } from '@inertiajs/inertia-vue3'



const props = defineProps({
     animal: {
        type: Object,
        default: () => ({}),
    },
});



</script>

<template>


    <Head title="Animal" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight inline-block	">
                Animal Information
            </h2> 
          
        </template>

          <template #default>
                <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                    
                    <!-- User Profile Tab Card -->
  <div class="flex flex-row rounded-lg border border-gray-200/80 bg-white p-6">
    <!-- Avaar Container -->
    <div class="relative">
      <!-- User Avatar -->
      <img class="w-40 h-40 rounded-md object-cover" src="https://api.lorem.space/image/face?w=150&h=150"
        alt="User" />


    </div>

    <!-- Meta Body -->
    <div class="flex flex-col px-6">
      <!-- Username Container -->
      <div class="flex h-8 flex-row">
        <!-- Username -->
        <a href="https://github.com/EgoistDeveloper/" target="_blank">
          <h2 class="text-lg font-semibold">{{ animal.name }}</h2>
        </a>

      </div>

      <!-- Meta Badges -->
      <div class="my-2 flex flex-row space-x-2">
        <!-- Badge Role -->
        <div class="flex flex-row">
          <svg class="mr-2 h-4 w-4 fill-gray-500/80" xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="24" height="24" viewBox="0 0 24 24">
            <path
              d="M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2M7.07,18.28C7.5,17.38 10.12,16.5 12,16.5C13.88,16.5 16.5,17.38 16.93,18.28C15.57,19.36 13.86,20 12,20C10.14,20 8.43,19.36 7.07,18.28M18.36,16.83C16.93,15.09 13.46,14.5 12,14.5C10.54,14.5 7.07,15.09 5.64,16.83C4.62,15.5 4,13.82 4,12C4,7.59 7.59,4 12,4C16.41,4 20,7.59 20,12C20,13.82 19.38,15.5 18.36,16.83M12,6C10.06,6 8.5,7.56 8.5,9.5C8.5,11.44 10.06,13 12,13C13.94,13 15.5,11.44 15.5,9.5C15.5,7.56 13.94,6 12,6M12,11A1.5,1.5 0 0,1 10.5,9.5A1.5,1.5 0 0,1 12,8A1.5,1.5 0 0,1 13.5,9.5A1.5,1.5 0 0,1 12,11Z" />
            </svg>

          <div class="text-xs text-gray-400/80 hover:text-gray-400">Fullstack Developer</div>
        </div>

        <!-- Badge Location -->
        <div class="flex flex-row">
          <svg class="mr-2 h-4 w-4 fill-gray-500/80" xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="24" height="24" viewBox="0 0 24 24">
            <path
              d="M12,6.5A2.5,2.5 0 0,1 14.5,9A2.5,2.5 0 0,1 12,11.5A2.5,2.5 0 0,1 9.5,9A2.5,2.5 0 0,1 12,6.5M12,2A7,7 0 0,1 19,9C19,14.25 12,22 12,22C12,22 5,14.25 5,9A7,7 0 0,1 12,2M12,4A5,5 0 0,0 7,9C7,10 7,12 12,18.71C17,12 17,10 17,9A5,5 0 0,0 12,4Z" />
            </svg>

          <div class="text-xs text-gray-400/80 hover:text-gray-400">Istanbul</div>
        </div>

        <!-- Badge Email-->
        <div class="flex flex-row">
          <svg class="mr-2 h-4 w-4 fill-gray-500/80" xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="24" height="24" viewBox="0 0 24 24">
            <path
              d="M12,15C12.81,15 13.5,14.7 14.11,14.11C14.7,13.5 15,12.81 15,12C15,11.19 14.7,10.5 14.11,9.89C13.5,9.3 12.81,9 12,9C11.19,9 10.5,9.3 9.89,9.89C9.3,10.5 9,11.19 9,12C9,12.81 9.3,13.5 9.89,14.11C10.5,14.7 11.19,15 12,15M12,2C14.75,2 17.1,3 19.05,4.95C21,6.9 22,9.25 22,12V13.45C22,14.45 21.65,15.3 21,16C20.3,16.67 19.5,17 18.5,17C17.3,17 16.31,16.5 15.56,15.5C14.56,16.5 13.38,17 12,17C10.63,17 9.45,16.5 8.46,15.54C7.5,14.55 7,13.38 7,12C7,10.63 7.5,9.45 8.46,8.46C9.45,7.5 10.63,7 12,7C13.38,7 14.55,7.5 15.54,8.46C16.5,9.45 17,10.63 17,12V13.45C17,13.86 17.16,14.22 17.46,14.53C17.76,14.84 18.11,15 18.5,15C18.92,15 19.27,14.84 19.57,14.53C19.87,14.22 20,13.86 20,13.45V12C20,9.81 19.23,7.93 17.65,6.35C16.07,4.77 14.19,4 12,4C9.81,4 7.93,4.77 6.35,6.35C4.77,7.93 4,9.81 4,12C4,14.19 4.77,16.07 6.35,17.65C7.93,19.23 9.81,20 12,20H17V22H12C9.25,22 6.9,21 4.95,19.05C3,17.1 2,14.75 2,12C2,9.25 3,6.9 4.95,4.95C6.9,3 9.25,2 12,2Z" />
            </svg>

          <div class="text-xs text-gray-400/80 hover:text-gray-400">who@am.i</div>
        </div>
      </div>

      <!-- Mini Cards -->
      <div class="mt-2 flex flex-row items-center space-x-5">
        <!-- Comments -->
        <div class="flex h-20 w-40 flex-col items-center justify-center rounded-md ">
          <div class="flex flex-row items-center justify-center">
            <span class="font-bold text-gray-600">{{ animal.type }}</span>
          </div>
          <div class="mt-2 text-sm text-gray-400">Type</div>
        </div>

        <div class="flex h-20 w-40 flex-col items-center justify-center rounded-md ">
          <div class="flex flex-row items-center justify-center">
            <span class="font-bold text-gray-600">{{ animal.breed }}</span>
          </div>
          <div class="mt-2 text-sm text-gray-400">Breed </div>
        </div>

        <div class="flex h-20 w-40 flex-col items-center justify-center rounded-md ">
          <div class="flex flex-row items-center justify-center">
            <span class="font-bold text-gray-600">{{ animal.gender }}</span>
          </div>
          <div class="mt-2 text-sm text-gray-400">Gender </div>
        </div>

        <!-- Projects -->
        <a href="#"
          class="flex h-20 w-40 flex-col items-center justify-center rounded-md ">
          <div class="flex flex-row items-center justify-center">
            <span class="font-bold text-gray-600">{{ animal.age }}</span>
          </div>

          <div class="mt-2 text-sm text-gray-400">Age</div>
        </a>

        <!-- Projects -->
        <a href="#"
          class="flex h-20 w-40 flex-col items-center justify-center rounded-md border border-dashed border-gray-200 transition-colors duration-100 ease-in-out hover:border-gray-400/80">
          <div class="flex flex-row items-center justify-center">
           

            <span class="font-bold text-gray-600"> 120K </span>
          </div>

          <div class="mt-2 text-sm text-gray-400">Downloads</div>
        </a>
      </div>
    </div>

    <!-- Right Actions Container -->
    <div class="w-100 flex flex-grow flex-col items-end justify-start">
      <div class="flex flex-row space-x-3">
        <!-- Follow Button -->
        <button
          class="flex rounded-md bg-blue-500 py-2 px-4 text-white transition-all duration-150 ease-in-out hover:bg-blue-600">
          <svg class="mr-2 fill-current" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
            version="1.1" width="24" height="24" viewBox="0 0 24 24">
            <path d="M19,13H13V19H11V13H5V11H11V5H13V11H19V13Z" /></svg>

          Add Disease
        </button>

       
      </div>
    </div>
  </div>
                </div>
        </template>
    </BreezeAuthenticatedLayout>



</template>