<template>
<div class="row">
    <div class="col-3" v-for="city,key in citiesList" :key="key" >
        <citycard @changeCity="handleSelctedCity" :name="city.name" />
    </div>
</div>
</template>

<script>
import citycard from "./citycard.vue";
export default {
    name:'citiesgrid',
    components:{
            citycard
    },
    data(){
        return{
            citiesList:[],
            selctedCity:''
        }
    },
    methods:{
        handleSelctedCity(name){
            console.log(name)
            this.selctedCity=name
            this.$emit('handleSelctedCity',name)
        }
    },
    created(){
        this.citiesList.push({
            name:'London'
        })
        this.citiesList.push({
            name:'Paris'
        })
        this.citiesList.push({
            name:'Berlin'
        })
        this.citiesList.push({
            name:'Tokyo'
        })
        this.citiesList.push({
            name:'Casablanca'
        })
        this.citiesList.push({
            name:'New York'
        })
    }
    
}
</script>

<style>

</style>