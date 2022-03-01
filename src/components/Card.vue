<template>
  <div class="grid md:grid-cols-2 gap-4 m-auto w-3/4">
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold md-4">Cas</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nouveaux:</span>
        {{ this.addCommas(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ this.addCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <div class="shadow-md bg-red-300 p-10 text-center rounded">
      <h3 class="text-3xl text-red-900 font-bold md-4">D&eacute;c&egrave;s</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nouveaux:</span>
        <span>&nbsp;{{ this.addCommas(stats.NewDeaths) }}</span>
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        <span>&nbsp;{{ this.addCommas(stats.TotalDeaths) }}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Card",
  props: ["stats"],
  methods: {
    addCommas(num) {
      const commas = num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      return commas;
    },
  },
};
</script>
