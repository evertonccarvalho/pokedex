<template>
  <div class="app">
      <div class="column is-half is-offset-one-quarter">
        <img src="./assets/logo.png" alt="">
        <hr>
        <h4 class="is-size-4"> Pokedex</h4>
        <input class="input is-rounded" type="text" name="" id="" placeholder="Buscar Pokemon pelo nome" v-model="busca">
        <button class="button is-normal is-success" id="busca-btn" @click="buscar">Buscar</button>
        
        <div v-for="(poke) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url"/>
      </div>
    </div>      
  </div>
  
</template>





<script>
import axios from 'axios'
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons:[],
      filteredPokemons:[],
      busca:''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("pegou a lista de pokemons");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
      
    })
  },

  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca =='' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }  
    }
  },
  components:{
    Pokemon
  },
  // computed:{
  //   resultadoBusca: function(){
  //     if(this.busca == '' || this.busca == ''){
  //       return this.pokemons;
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name ==this.busca)
  //     }      
  //   }
  // }
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
#busca-btn{
  margin-top: 2%;
}
</style>
