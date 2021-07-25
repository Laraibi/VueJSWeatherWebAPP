<template>
    <div class="card pointer" >
        <div class="card-header">
            <h2 class="card-title">{{name}}</h2>
        </div>
        <div class="card-body">
            <button class="btn btn-warning" @click="changeSelectedCity">click me</button>
            <img :src="src" alt="">
        </div>
    </div>
</template>

<script>
export default {
  name: "citycard",
  props:{
      name:{
          type:String,
          value:''
      },
  },
  methods:{
      changeSelectedCity(){
        //   console.log(this.name)
          this.$emit('changeCity',this.name)
      }
  }
};
</script>

<style>
</style>