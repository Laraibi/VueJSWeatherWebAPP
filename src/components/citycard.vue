<template>
  <div class="">
    <h6 class="card-title btn btn-outline-info text-nowrap" @click="changeSelectedCity">
      {{ name }}
    </h6>
  </div>
</template>

<script>
export default {
  name: "citycard",
  props: {
    name: {
      type: String,
      value: "",
    },
  },
  methods: {
    changeSelectedCity() {
      //   console.log(this.name)
      this.$emit("changeCity", this.name);
    },
  },
};
</script>

<style>
</style>