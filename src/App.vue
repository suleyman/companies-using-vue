<template>
  <div class="bg-gray-100">
    <div class="container mx-auto">
      <section class="pt-12 md:px-0 px-12 grid md:grid-cols-4 grid-cols-1 gap-8">
        <Company v-for="(company, index) in companies" :company-data="company" />
      </section>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Company from "./components/Company.vue";
import companiesData from "./data/companies.json";
import { ICompany } from "./interfaces/company";

export default defineComponent({
  name: "App",
  components: {
    Company,
  },
  setup: () => {
    let companies = ref<Array<ICompany>>([]);
    for (let i = 0; i < 24; i++) {
      companies.value.push(companiesData[0]);
    }
    return { companies };
  },
});
</script>
