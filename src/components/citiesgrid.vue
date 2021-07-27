<template>
  <div class="row .overflow-auto">
    <div class="col-3" v-for="(city, key) in citiesList" :key="key">
      <citycard @changeCity="handleSelctedCity" :name="city.name" />
    </div>
  </div>
</template>

<script>
// import axios from "axios";
import citycard from "./citycard.vue";
export default {
  name: "citiesgrid",
  components: {
    citycard,
  },
  data() {
    return {
      citiesList: [],
      selctedCity: "",
      LocalCities:[]
    };
  },
  methods: {
    handleSelctedCity(name) {
      console.log(name);
      this.selctedCity = name;
      this.$emit("handleSelctedCity", name);
    },
  },
  created() {
    this.citiesList.push({
      name: "London",
    });
    this.citiesList.push({
      name: "Paris",
    });
    this.citiesList.push({
      name: "Berlin",
    });
    this.citiesList.push({
      name: "Tokyo",
    });
    this.citiesList.push({
      name: "Casablanca",
    });
    this.citiesList.push({
      name: "New York",
    });
    this.citiesList.push({
      name: "Bangkok",
    });
    // axios.get("city.list.json").then((res) => (this.LocalCities = res.data));
  },
};
</script>

<style>
</style>