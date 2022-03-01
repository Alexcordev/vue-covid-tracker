<template>
  <Header />
  <main v-if="!loading">
    <DataTitle :text="this.title" :dataDate="this.dataDate" />
    <div class="flex flex-col align-center justify-center text-center w-100">
      <Card :stats="this.stats" />
      <CountrySelect
        @get-country="getCountryData"
        :countries="this.countries"
      />
    </div>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Veuillez patienter...</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="wait_img" />
  </main>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import DataTitle from "@/components/DataTitle.vue";
import Card from "@/components/Card.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "HomeView",
  components: {
    Header,
    DataTitle,
    Card,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/1486.gif"),
    };
  },
  methods: {
    async getCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
  },
  //LifeCycle hook that execute at runtime
  async created() {
    const data = await this.getCovidData();
    console.log(data);
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
