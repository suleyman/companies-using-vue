<template>
  <div class="relative animate-fade-in-up bg-white py-6 px-6 rounded-3xl w-full my-4 shadow-xl">
    <div class="text-white flex items-center absolute p-2 rounded-full shadow-xl bg-green-400 left-4 -top-6">
      <!-- Logo  -->
      <img :src="`/company-logos/${companyData.logo}`" class="rounded-full" width="64" height="64" />
    </div>
    <div class="mt-12">
      <p class="text-xl font-semibold my-2">{{ companyData.name }}</p>
      <div class="flex space-x-2 text-gray-400 text-sm">
        <!-- svg  -->
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
          />
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
        </svg>
        <p>{{ companyData.location }}</p>
      </div>
      <div class="flex space-x-2 text-gray-400 text-sm my-3">
        <!-- svg  -->
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
          />
        </svg>
        <p>
          <a :href="companyData.website + '?utm_source=companies-using-vue'" target="_blank" class="hover:text-blue-700">{{
            companyData.website
          }}</a>
        </p>
      </div>
      <div class="flex space-x-2 text-gray-400 text-sm my-3">
        <!-- svg  -->
        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 64 64" class="h-5 w-5">
          <path
            fill="currentColor"
            d="M56.5,19.5L36,1.6c-2.4-2.1-5.9-2.1-8,0L7.5,19.5c-1.3,1.3-2.1,2.9-2.1,4.8v33.6c0,3.5,2.7,6.1,6.1,6.1h9.1
	c3.5,0,6.1-2.7,6.1-6.1V46.1c0-0.5,0.3-0.8,0.8-0.8h9.1c0.5,0,0.8,0.3,0.8,0.8v11.7c0,3.5,2.7,6.1,6.1,6.1h9.1
	c3.5,0,6.1-2.7,6.1-6.1V24.3C58.7,22.4,57.9,20.8,56.5,19.5z M53.3,57.9c0,0.5-0.3,0.8-0.8,0.8h-9.1c-0.5,0-0.8-0.3-0.8-0.8V46.1
	c0-3.5-2.7-6.1-6.1-6.1h-9.1c-3.5,0-6.1,2.7-6.1,6.1v11.7c0,0.5-0.3,0.8-0.8,0.8h-9.1c-0.5,0-0.8-0.3-0.8-0.8V24.3
	c0-0.3,0-0.5,0.3-0.5L31.5,5.9c0.3-0.3,0.8-0.3,1.1,0L53,23.8c0.3,0,0.3,0.3,0.3,0.5L53.3,57.9L53.3,57.9z"
          />
        </svg>

        <p>
          <span class="mr-4">Remote</span>
          <span class="text-green-500 font-bold" v-if="companyData.isRemote">YES</span>
          <span class="text-red-500 font-bold" v-if="!companyData.isRemote">NO</span>
        </p>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { ref, defineComponent, PropType, computed } from "vue";
import { ICompany } from "../interfaces/company";

export default defineComponent({
  name: "Company",
  props: {
    companyData: {
      type: Object as PropType<ICompany>,
      required: true,
    },
  },
  setup: (props) => {
    const getDescription = computed(() => {
      return props.companyData?.description?.substr(0, 80) || null;
    });

    return { getDescription };
  },
});
</script>
