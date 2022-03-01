<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select mt-10 block w-3/4 border p-3 rounded m-auto"
  >
    <option value="0">Choisir le pays</option>
    <option v-for="country in countries" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>
<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);

      this.$emit("get-country", country);
    },
  },
};
</script>
