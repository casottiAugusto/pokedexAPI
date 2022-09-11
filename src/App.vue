<template>
  <div class="app">
    <h1>PokeDex</h1>
  </div>
</template>

<script>
import axios from 'axios';

export default{
  name:'App',
  data(){
    return{
      pokemons:[]
    }
  },
  created:function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0").then(dados=>{
      
      this.pokemons=dados.data.results;
    }).catch(err=>{
      console.log(err)
    })
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
