<template>
  <div class="row">
    <citiesgrid @handleSelctedCity="handleSelctedCity" />
  </div>
  <div class="row">
    {{ weatherData }}
  </div>
  <div class="row" v-if="city.length > 0">
    <div class="col-3">
      <img :src="iconUrl" alt="" class="img" />
    </div>
    <div class="col-3">
        <small> Meteo: </small>{{ weatherData.weather[0].description }}
    </div>
    <div class="col-3">
        <small> Temperature: </small>{{ weatherData.main.temp }}
    </div>
    <div class="col-3">
        <small> Local Time: </small>{{ time }} 
    </div>
  </div>
</template>
<script>
import axios from "axios";
import citiesgrid from "./citiesgrid.vue";
let moment = require("moment");
export default {
  name: "weatherForm",
  components: {
    citiesgrid,
  },
  data() {
    return {
      city: "",
      weatherData: [],
      iconUrl: "",
      time: "",
    };
  },
  methods: {
    load() {
      axios
        .get("http://api.openweathermap.org/data/2.5/weather", {
          params: {
            q: this.city,
            appid: "d67c1011504cc238bb5af61408c16e31",
            units: "metric",
            lang: "fr",
          },
        })
        .then((res) => {
          this.weatherData = res.data;
          let iconCode = res.data.weather[0].icon;
          this.time = moment
            .utc(this.weatherData.dt, "X")
            .add(this.weatherData.timezone, "seconds")
            .format("YYYY-MM-DD HH:mm:ss");
          this.iconUrl = "http://openweathermap.org/img/w/" + iconCode + ".png";
        });
    },
    handleSelctedCity(name) {
      this.city = name;
      this.load();
    },
  },
};
</script>
<style>
</style>