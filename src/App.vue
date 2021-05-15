<template>
  <div class="bg-gray-100 pt-12 min-h-screen">
    <div class="container mx-auto p-4 md:p-0">
      <section class="p-12 bg-white rounded-3xl">
        <form class="flex lg:items-center flex-col lg:flex-row">
          <div class="mr-12">
            <div class="flex justify-between items-center cursor-pointer" @click="isRemote = !isRemote">
              <label class="mr-4">Remote</label>
              <div
                class="w-14 h-8 flex items-center bg-gray-300 rounded-full p-1 duration-300 ease-in-out"
                :class="{ 'bg-green-400': isRemote }"
              >
                <div
                  class="bg-white w-6 h-6 rounded-full shadow-md transform duration-300 ease-in-out"
                  :class="{ 'translate-x-6': isRemote }"
                ></div>
              </div>
            </div>
          </div>
          <div class="mt-4 lg:mt-0">
            <label class="mr-4">Location</label>
            <div class="relative inline-block text-gray-700">
              <select
                class="w-full h-10 pl-3 pr-6 cursor-pointer text-base placeholder-gray-600 border rounded-lg appearance-none outline-none focus:ring-1 focus:ring-green-400"
                v-model="selectedLocation"
              >
                <option :value="null">All</option>
                <option v-for="location in companyLocations" :value="location">{{ location }}</option>
              </select>
              <div class="absolute inset-y-0 right-0 flex items-center px-2 pointer-events-none">
                <svg class="w-4 h-4 fill-current" viewBox="0 0 20 20">
                  <path
                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                    clip-rule="evenodd"
                    fill-rule="evenodd"
                  ></path>
                </svg>
              </div>
            </div>
          </div>
          <div class="mt-4 lg:mt-0 lg:ml-auto" v-if="filteredCompanies && filteredCompanies.length > 0">
            <span class="text-green-400 font-bold">{{ filteredCompanies.length }}</span> companies listed
          </div>
        </form>
      </section>
      <transition>
        <section class="mt-12 grid md:grid-cols-4 grid-cols-1 gap-8">
          <Company v-for="(company, index) in filteredCompanies" :company-data="company" />
        </section>
      </transition>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, Ref } from "vue";
import { ICompany } from "./interfaces/company";
import Company from "./components/Company.vue";
import companiesData from "./data/companies.json";
import _filter from "lodash/filter";
import _uniq from "lodash/uniq";

export default defineComponent({
  name: "App",
  components: {
    Company,
  },
  setup: () => {
    const companies: Ref<ICompany[]> = ref(companiesData);
    const companyLocations = _uniq(companies.value.map((company: ICompany) => company.location));

    const selectedLocation: Ref<string | null> = ref(null);
    const isRemote: Ref<boolean> = ref(true);

    const filteredCompanies = computed(() => {
      return _filter(companies.value, {
        isRemote: isRemote.value,
        ...(selectedLocation.value ? { location: selectedLocation.value } : {}),
      });
    });

    return {
      companies,
      companyLocations: new Set(companyLocations),
      selectedLocation,
      isRemote,
      filteredCompanies,
    };
  },
});
</script>
