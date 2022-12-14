<script setup>
import BreezeAuthenticatedLayout from "@/Layouts/Authenticated.vue";
import AnimalDetailsField from "./AnimalDetailsField.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { Inertia } from "@inertiajs/inertia";
import { Link } from "@inertiajs/inertia-vue3";
import { useForm } from "@inertiajs/inertia-vue3";
import { ref } from "vue";
import Swal from "sweetalert2";

const props = defineProps({
  animal: {
    type: Object,
    default: () => ({}),
  },
  diseases: {
    type: Array,
  },
});

let isActive = ref(false);
let modalTitle = "Add Disease";

let form = useForm({
  animal_id: null,
  disease_id: null,
});

function addDisease(animal_id) {
  form.animal_id = animal_id;
  form.post(route("addDisease"), {
    onSuccess: (response) => {
      Swal.fire("Disease has been added!", "Success!", "success");
    },
  });
}

function removeDisease(animal_id, disease_id) {
  form.animal_id = animal_id;
  form.disease_id = disease_id;
  Swal.fire({
    title: "Are you sure?",
    text: "You won't be able to revert this!",
    icon: "warning",
    showCancelButton: true,
    confirmButtonColor: "#3085d6",
    cancelButtonColor: "#d33",
    confirmButtonText: "Yes, remove it!",
  }).then((result) => {
    if (result.isConfirmed) {
      form.delete(route("removeDisease"));
      Swal.fire("Deleted!", "Disease has been removed.", "success");
    }
  });
}
</script>

<template>
  <Head title="Animal" />

  <BreezeAuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight block">
        Animal Information
      </h2>
    </template>

    <template #default>
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <!-- User Profile Tab Card -->
        <div
          class="
            flex flex-row
            rounded-lg
            border border-gray-200/80
            bg-white
            p-6
          "
        >

          <div class="relative"></div>
          <div class="flex flex-col">
            <div class="flex h-8 flex-row">
              <h2 class="text-lg font-semibold">{{ animal.name }}</h2>
            </div>
            <div class="my-2 flex flex-row space-x-2">
              <div class="flex flex-row">
                <div class="text-base text-gray-600">
                  Status: <span v-if="animal.diseases.length"> Sick</span>
                  <span v-else> Healthy</span>
                </div>
              </div>
            </div>

            <div class="mt-2 flex flex-row items-center">
              <AnimalDetailsField :title="'Type'" :animalInfo="animal.type" />
              <AnimalDetailsField :title="'Breed'" :animalInfo="animal.breed" />
              <AnimalDetailsField :title="'Gender'" :animalInfo="animal.gender" />
              <AnimalDetailsField :title="'Age'" :animalInfo="animal.age" />
            </div>
          </div>

          <div class="w-100 flex flex-grow flex-col items-end justify-start">
            <div class="flex flex-row space-x-3">
              <button
                @click="isActive = true"
                class="
                  flex
                  rounded-md
                  bg-blue-500
                  py-2
                  px-4
                  text-white
                  transition-all
                  duration-150
                  ease-in-out
                  hover:bg-blue-600
                "
              >
                <svg
                  class="mr-2 fill-current"
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  version="1.1"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                >
                  <path d="M19,13H13V19H11V13H5V11H11V5H13V11H19V13Z" />
                </svg>
                Add Disease
              </button>
            </div>
          </div>
        </div>


        <div v-if="animal.diseases.length"
          class="
            max-w-7xl
            mx-auto
            my-5
            py-6
            px-4
            sm:px-6
            lg:px-8
            bg-white
            shadow
          "
        >
          <h1 class="text-lg font-semibold text-center">Diseases</h1>
          <table class="min-w-max w-full table-fixed mt-3">
            <thead>
              <tr
                class="
                  bg-gray-200
                  text-gray-600
                  uppercase
                  text-lg
                  leading-normal
                "
              >
                <th class="py-3 px-6 text-left">Name</th>
                <th class="py-3 px-6 text-left">Description</th>
                <th class="py-3 px-6 text-center">Actions</th>
              </tr>
            </thead>
            <tbody class="text-gray-600 text-lg font-light">
              <tr
                class="border-b border-gray-200 hover:bg-gray-100"
                v-for="disease in animal.diseases"
                :key="disease"
              >
                <td class="py-3 px-6 text-left whitespace-nowrap">
                  <div class="flex items-center">
                    <span class="font-medium">{{ disease.name }}</span>
                  </div>
                </td>
                <td class="py-3 px-6 text-left text-base">
                  <div class="flex items-center">
                    <span>{{ disease.description }}</span>
                  </div>
                </td>

                <td class="py-3 px-6 text-center">
                  <div class="flex item-center justify-center">
                    <div
                      class="
                        w-4
                        mr-2
                        transform
                        hover:text-purple-500 hover:scale-110
                        cursor-pointer
                      "
                      @click="removeDisease(animal.id, disease.id)"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                        />
                      </svg>
                    </div>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- modal -->
        <div class="container mx-auto">
          <div class="flex justify-center">
            <div
              v-show="isActive"
              class="
                absolute
                inset-0
                flex
                items-center
                justify-center
                bg-gray-700 bg-opacity-50
              "
              @click.self="isActive = false"
            >
              <div class="max-w-2xl p-6 bg-white rounded-md shadow-xl w-screen">
                <div class="flex items-center justify-between">
                  <h3 class="text-2xl">{{ modalTitle }}</h3>
                  <svg
                    @click="isActive = false"
                    xmlns="http://www.w3.org/2000/svg"
                    class="w-8 h-8 text-red-900 cursor-pointer"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
                    />
                  </svg>
                </div>
                <form @submit.prevent="addDisease(animal.id)">
                  <div class="my-3">
                    <label
                      for="Diseases"
                      class="mb-3 block text-base font-medium text-[#07074D]"
                    >
                      Diseases:
                    </label>
                    <select
                      v-model="form.disease_id"
                      class="
                        w-full
                        rounded-md
                        border border-[#e0e0e0]
                        bg-white
                        py-3
                        px-6
                        text-base
                        font-medium
                        text-[#6B7280]
                        outline-none
                        focus:border-[#6A64F1] focus:shadow-md
                      "
                    >
                      <option value="">--Please select type--</option>
                      <option
                        v-for="disease in diseases"
                        :key="disease"
                        :value="disease.id"
                      >
                        {{ disease.name }}
                      </option>
                    </select>
                  </div>
                  <div v-if="form.errors.disease_id">
                    {{ form.errors.disease_id }}
                  </div>

                  <div class="mt-4">
                    <button
                      @click="isActive = false"
                      class="
                        px-6
                        py-2
                        text-blue-800
                        border border-blue-600
                        rounded
                      "
                    >
                      Cancel
                    </button>
                    <button
                      type="submit"
                      class="px-6 py-2 ml-2 text-blue-100 bg-blue-600 rounded"
                    >
                      Add
                    </button>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </template>
  </BreezeAuthenticatedLayout>
</template>
