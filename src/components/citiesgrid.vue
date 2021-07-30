<template>
  <div class="row .overflow-auto">
    <div class="col-3 my-2" v-for="(city, key) in citiesList" :key="key">
      <citycard @changeCity="handleSelctedCity" :name="city.name" />
    </div>
    <div class="col-3 my-2">
      <div class="row">
        <div class="col-10">
          <input
            type="text"
            v-model.lazy="selctedCity"
            id=""
            class="form-control"
            placeholder="City,Country"
          />
        </div>
        <button class="btn btn-success col-2">
          <i class="bi bi-search"></i>
        </button>
      </div>
      <div class="row">
        <div class="col-12">
          <select name="" id="" class="form-select" @change="handleSelctedCity" v-model="selctedCity">
              <option v-for="historyitem,key in history" :key="key" :value="historyitem">{{historyitem}}</option>
          </select>
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
  props:{
    history:{
      type:Array,
      value:[]
    }
  },
  data() {
    return {
      citiesList: [],
      selctedCity: "",
      LocalCities: [],
    };
  },
  methods: {
    handleSelctedCity(name=this.selctedCity) {
      // console.log(typeof name);
      if(typeof name === "object"){
        this.selctedCity = name.target.value;
      }else{
        this.selctedCity = name;
      }
      this.$emit("handleSelctedCity",  this.selctedCity);
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