<template>
  <div id="pokemon">
    
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="correntIMG" alt="Placeholder image" />
        </figure>
      </div>
      <div class="media-content">
        <p class="title is-4">{{num}}-{{ upper(name) }}</p>
        <p class="subtitle is-6">{{ pokemons.type }}</p>
      </div>
      <div class="card-content">
        <div class="content">
          <button class="button is-small is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
        

          <br />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemons.type = res.data.types[0].type.name;
      this.pokemons.front = res.data.sprites.front_default;
      this.pokemons.back = res.data.sprites.back_default;
      this.correntIMG=this.pokemons.front;
      
      
    });
  },
  data() {
    return {
      isFront:true,
      correntIMG:'',
      pokemons: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  methods: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
    mudarSprite:function () {
      if (this.isFront) {
        this.isFront=false;
        this.correntIMG=this.pokemons.back;
        
      }else{
        this.isFront=true;
        this.correntIMG=this.pokemons.front;

      }
      
    }
  },
};
</script>

<style>
 #pokemon{
  margin-top:2%;
 
}
</style>