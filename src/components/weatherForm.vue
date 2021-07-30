<template>
  <div>
    <div class="row" id="table" v-if="city.length > 0">
      <div class="col-lg-3 col-sm-4">
        <div class="card">
          <div class="card-header">
            <h6 class="card-title">{{ city }},{{ weatherData.sys.country }}</h6>
          </div>
          <div class="card-body">
            <div class="row justify-content-center">
              <div class="col-7">
                <img
                  class=""
                  :src="
                    'https://www.countryflags.io/' +
                    weatherData.sys.country +
                    '/shiny/64.png'
                  "
                  alt=""
                />
              </div>
              <div class="row">
                <div class="col-12 justify-content-center">{{ time }}</div>
              </div>
              <div
                class="row border-top my-1 border-bottom border-1 border-dark"
              >
                <div class="col-12 justify-content-center font-weight-bold">
                  {{ weatherData.main.temp.toFixed(0) }} &#8451;
                </div>
              </div>
              <div class="row my-1">
                <div class="col-6 justify-content-center font-weight-bold">
                  {{ weatherData.weather[0].description }}
                </div>
                <div class="col-6 justify-content-center font-weight-bold">
                  <img class="image-fluid img" :src="iconUrl" alt="" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-lg-9 col-sm-8">
        <div class="card">
          <div class="card-header">
            <h6 class="card-title">Previsions pendant 5 prochains jours</h6>
          </div>
          <div class="card-body">
            <line-chart :chartData="chartData" />
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <citiesgrid @handleSelctedCity="handleSelctedCity" :history="history" />
    </div>
  </div>
</template>
<script>
import axios from "axios";
import citiesgrid from "./citiesgrid.vue";
import LineChart from "./LineChart.vue";
let moment = require("moment");
function arrayAverage(arr) {
  var total = 0;
  arr.forEach((element) => {
    total += element;
  });
  return (total / arr.length).toFixed(0);
}
export default {
  name: "weatherForm",
  components: {
    citiesgrid,
    LineChart,
  },
  data() {
    return {
      city: "",
      weatherData: [],
      iconUrl: "",
      time: "",
      forcast: {},
      chartData: {},
      history: [],
    };
  },
  watch: {
    city() {
      // this.history.push(this.city);
    },
  },
  methods: {
    load() {
      return new Promise((resolve) => {
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
            this.iconUrl =
              "http://openweathermap.org/img/w/" + iconCode + ".png";
            // this.loadForcast();
            resolve();
          });
      });
    },
    handleSelctedCity(name) {
      // this.history.push(name)
      this.city = name;
      this.load().then(() => {
        this.loadForcast().then(() => {
          if (!this.history.includes(this.city)) {
            this.history.push(this.city);
          }
        });
      });
      // ;
    },
    loadForcast() {
      return new Promise((resolve) => {
        axios
          .get("http://api.openweathermap.org/data/2.5/forecast", {
            params: {
              q: this.city,
              appid: "d67c1011504cc238bb5af61408c16e31",
              units: "metric",
              lang: "fr",
            },
          })
          .then((res) => {
            let list = res.data.list;
            list.forEach((forcast) => {
              if (
                Object.keys(this.forcast).includes(forcast.dt_txt.split(" ")[0])
              ) {
                this.forcast[forcast.dt_txt.split(" ")[0]].push(
                  forcast.main.temp
                );
              } else {
                this.forcast[forcast.dt_txt.split(" ")[0]] = [
                  forcast.main.temp,
                ];
              }
            });
            // console.log(this.forcast.length);
            this.chartData = {
              labels: Object.keys(this.forcast),
              datasets: [
                {
                  label: "forcast",
                  data: Object.values(this.forcast).map((temps) =>
                    arrayAverage(temps)
                  ),
                  fill: false,
                  borderColor: "rgb(75, 192, 192)",
                },
              ],
            };
            resolve();
          });
      });
    },
  },
};
</script>
<style>
</style>