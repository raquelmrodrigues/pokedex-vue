<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
        <PokemonComponent :name="poke.name" :url="poke.url" :num="index + 1"/> 
      </div>
    </div>


  </div>
</template>

<script>
  import axios from 'axios';
  import PokemonComponent from './components/PokemonComponent.vue';

export default {
  name: 'App',

  data() {
    return {
      pokemons: []
    }
  },

  // assim que a pagina é carregada faz uma requisição a api que retorna os 151 pokemons
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151offset=0").then(res => {
      this.pokemons = res.data.results;
    })
  },

  components: {
      PokemonComponent
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
