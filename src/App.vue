<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <hr>
      <p class="is-size-4">POKEDEX</p>

      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="query">
      <button class="button is-fullwidth is-success" id="btnSearch" @click="search">Buscar</button>

      <div v-for="(poke, index) in filterPokemons" :key="poke.name">
        <pokemon
            :name="poke.name"
            :url="poke.url"
            :number="index + 1"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import pokemon from './components/Pokemon';
export default {
  name: 'App',
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
        .then(res => {
          this.pokemons = res.data.results;
          this.filterPokemons = res.data.results;
        });
  },
  data() {
    return {
      pokemons: [],
      filterPokemons: [],
      query: '',
    }
  },
  components: {
    pokemon
  },
  methods: {
    search: function() {
      if (this.query == '' ||  this.query == '') {
        this.filterPokemons = this.pokemons
        return;
      }

      this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.query.toLowerCase());
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
#btnSearch {
  margin-top: 2%;
}
</style>
