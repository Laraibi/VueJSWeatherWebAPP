<template>
  <div class="row .overflow-auto">
    <div class="col-6">
      <div class="row">
        <div class="col" v-for="(city, key) in citiesList" :key="key">
          <citycard @changeCity="handleSelctedCity" :name="city.name" />
        </div>
      </div>
    </div>
    <div class="col-6">
      <div class="row">
        <div class="col">
          <div class="row">
            <div class="col-10">
              <input
                type="text"
                @change="handleSelctedCity"
                v-model.lazy="selctedCity"
                id=""
                class="form-control"
                placeholder="City,Country"
              />
            </div>
            <div class="col-2">
              <button class="btn btn-outline-success">
                <i class="bi bi-search"></i>
              </button>
            </div>
          </div>
          <div class="row">
            <div class="col-12">
              <div class="card">
                <div class="card-header">
                  <h6 class="card-title">Historique</h6>
                </div>
                <div class="card-body">
                  <select
                    name=""
                    id=""
                    class="form-select"
                    @change="handleSelctedCity"
                    v-model="selctedCity"
                  >
                    <option
                      v-for="(historyitem, key) in history"
                      :key="key"
                      :value="historyitem"
                    >
                      {{ historyitem }}
                    </option>
                  </select>
                  <ul class="list-group">
                    <li
                      v-for="(historyitem, key) in history"
                      :key="key"
                      class="list-group-item"
                    >
                      {{ historyitem }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
  props: {
    history: {
      type: Array,
      value: [],
    },
  },
  data() {
    return {
      citiesList: [],
      selctedCity: "",
      LocalCities: [],
    };
  },
  methods: {
    handleSelctedCity(name = this.selctedCity) {
      // console.log(typeof name);
      if (typeof name === "object") {
        this.selctedCity = name.target.value;
      } else {
        this.selctedCity = name;
      }
      this.$emit("handleSelctedCity", this.selctedCity);
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
  },
};
</script>

<style>
</style>