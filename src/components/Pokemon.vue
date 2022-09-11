<template>
  <div>
    <h1>{{num}} {{upper(name) }}</h1>
    <small>{{url}}</small>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  created:function () {
    axios.get(this.url).then(res=>{
      
      this.pokemons.type=res.data.types[0].type.name;
      this.pokemons.front=res.data.sprites.front_default;
      this.pokemons.back=res.data.sprites.back_default;
      console.log(this.pokemons);
    })
    
  },
  data(){
    return{
      pokemons:{}
    }
  },
  props:{
    num:Number,
    name:String,
    url:String,
   
  },
  methods:{
   upper:function (value) {
    var newName =value[0].toUpperCase() +value.slice(1);
    return newName;
    
   }
  }


}
</script>

<style>

</style>