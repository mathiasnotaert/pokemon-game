<template>
  <div id="app" class="container appcontainer">
    <insert-pokemon @check-pokemon="checkPokemon"/>
    <pokemon-overview :pokemons="pokemons" :pokemons-found="pokemonsFound" :game-started="gameStarted" @stop-game="stopGame"/>
  </div>
</template>

<script>

import axios from 'axios';
import insertPokemon from './components/pokemon-overview/insertPokemon.vue';
import PokemonOverview from './components/pokemon-overview/PokemonOverview.vue';

export default {
  components: { insertPokemon, PokemonOverview },
  name: 'App',
  data() {
    return {
      pokemons: {},
      pokemonImages: {},
      pokemonData: {},
      pokemonsFound: [],
      gameStarted: false,
    }
  },
  mounted () {
    axios
      .get('https://pokeapi.co/api/v2/pokemon?limit=151')
      .then(response => (
        this.pokemons = response.data.results
      ));
  },
  methods: {
    checkPokemon(pokemon) {
      if (!this.gameStarted) {
        this.gameStarted = true;
      }
      const pokemons = this.pokemons;
      const insertedPokemon = pokemon;
      let isValidPokemon = false;

      const pokemonArr = pokemons.filter(pokemon => pokemon.name == insertedPokemon);

      if (pokemonArr.length) {
        isValidPokemon = true;
        this.pokemonsFound.push(pokemonArr[0].name);
      }
      return isValidPokemon;
    },
    stopGame() {
      this.gameStarted = false;
    },
  }
}
</script>
<style>
@import'~bootstrap/dist/css/bootstrap.css';
body {
  background-color: #033860;
  color: white;
}
</style>
