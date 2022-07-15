<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <hr>
      <p class="is-size-4">POKEDEX</p>
      <div v-for="(poke, index) in pokemons" :key="index">
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
        });
  },
  data() {
    return {
      pokemons: []
    }
  },
  components: {
    pokemon
  },
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
