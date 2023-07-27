<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
      <input type="text" class="input is-rounded" placeholder="Buscar Pokemon" v-model="busca">
      
      <div v-for="(poke, index) in resultadoBusca" :key="index">
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
      pokemons: [],
      busca: ''
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
  },

  computed: {
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
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

</style>
