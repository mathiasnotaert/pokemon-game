<template>
  <div class="row pokemon-overview">
    <div class="row justify-content-center mt-4" >
        <p class="col-md-3 text-center">Pokémon found: {{ pokemonsFound.length }} / 151</p>
        <div class="col-md-3 text-center">Time left: <span id="time">15:00</span></div>
    </div>
    <pokemon-card v-for="(pokemon, index) in pokemons" 
    :key="pokemon.name" 
    :name="pokemon.name" 
    :url="pokemon.url" 
    :number="index + 1"
    :pokemons-found="pokemonsFound" />
  </div>
</template>

<script>

import PokemonCard from './PokemonCard.vue';

export default {
  components: { PokemonCard },
name: 'PokemonOverview',
data() {
    return {
      gameTime: ""
    }
  },
props: {
    pokemons: {
      type: Array
    },
    pokemonsFound: {
      type: Array
    },
    gameStarted: {
      type: Boolean
    },
  },
  watch: {
    gameStarted: function () {
      const duration = 60 * 15;
      const display = document.querySelector('#time');
      let timer = duration, minutes, seconds;
    setInterval(function () {
        minutes = parseInt(timer / 60, 10)
        seconds = parseInt(timer % 60, 10);

        minutes = minutes < 10 ? "0" + minutes : minutes;
        seconds = seconds < 10 ? "0" + seconds : seconds;

        this.gameTime = minutes + ":" + seconds;

        display.textContent = minutes + ":" + seconds;

        if (--timer < 0) {
            timer = duration;
            this.$emit('stop-game');
        }
    }, 1000);
    }
  }
}
</script>

<style scoped>
.pokemon-overview {
  margin: 0 auto;
}
</style>