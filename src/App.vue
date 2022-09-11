<template>

  <div class="app">

    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokebolas.png" alt="pokebolas">
      <input type="text" placeholder="Buscar Pokemom com o nome" class="input is-rounded" v-model="busca">
      <button class="button is-rounded" id="buscaBTN" @click="buscar">Buscar</button>
     
     
     <div v-for="(poke,index) in filterpoke " :key="poke.url">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
    

    </div>

     </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default{
  name:'App',
  data(){
    return{
      pokemons:[],
      busca:'',
      filterpoke:[]

    }
  },
  created:function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(dados=>{
      
      this.pokemons=dados.data.results;
      this.filterpoke=dados.data.results

    }).catch(err=>{
      console.log(err)
    })
  },
  components:{
    Pokemon
  },
  computed:{
    resultBusca:function () {
      if(this.busca==""|| this.busca==""){
        return this.pokemons
     }else{
       return this.pokemons.filter(pokemon =>pokemon.name==this.busca)
     }
    }
  },methods:{
    buscar:function () {
      this.filterpoke=this.pokemons;
       if(this.busca==""|| this.busca==""){

       this.filterpoke=this.pokemons;
        
     }else{
      this.filterpoke=this.pokemons.filter(pokemon =>pokemon.name==this.busca);
       
     }

      
    }
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
#buscaBTN{
  margin-top: 1%;
}
</style>
