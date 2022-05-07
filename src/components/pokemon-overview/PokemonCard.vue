<template>
  <div class="col-sm-1 pokemon-card" :class="{ 'pokemon-card--hidden': isFound }">
    <base-card :name="name" :img="this.pokemonImage" :id="this.number" v-if="isFound"/>
    <hidden-card :name="name" v-else />
  </div>
</template>

<script>

import axios from 'axios';
import HiddenCard from '../layout/HiddenCard.vue';
import BaseCard from '../layout/BaseCard.vue';

export default {
  components: { BaseCard, HiddenCard },
  name: 'PokemonCard',
  data() {
      return {
        pokemonImage: "",
      }
    },
  props: {
      name: {
        type: String,
        default: ""
      },
      url: {
        type: String,
        default: ""
      },
      number: {
        type: Number,
      },
      pokemonsFound: {
        type: Array,
      },
    },
    mounted () {
      axios
        .get(this.pokemonApi)
        .then(response => (
          this.pokemonImage = response.data.sprites.front_default
        ));
    },
  computed: {
    pokemonApi() {
      return 'https://pokeapi.co/api/v2/pokemon/' + this.number + '/';
    },
    isFound() {
      return this.pokemonsFound.filter(pokemon => pokemon == this.name).length ? true : false;
    }
}

}
</script>

<style scoped>
.pokemon-card {
  border: 1px solid #004385;
  height: 80px;
  width: 80px;
  padding: 0;
}
</style>
