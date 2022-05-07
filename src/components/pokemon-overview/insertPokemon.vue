<template>
<form class="form-inline mt-1">
        <div class="form-group pokemon-form-group">
        <input name="pokemon" class="pokemon-form" v-model="pokemonInput" autocomplete="off">
        <button @click="checkPokemon" class="btn btn-outline-light pokemon-btn" >Check</button>
        </div>
</form>
       
</template>

<script>
export default {
name: 'InsertPokemon',
  data() {
    return {
      pokemonInput: "",
    }
  },
  methods: {
      checkPokemon(e) {
          e.preventDefault();
          this.$emit('check-pokemon', this.pokemonInput);
          this.pokemonInput = "";
      }
  }
}
</script>

<style scoped>
.pokemon-form-group {
  display: flex;
  justify-content: center;
}
.pokemon-form {
  background-color: #033860;
  color: white;
  border: 1px solid white;
  padding: 5px;
  margin-right: 10px;
}

.pokemon-form:focus {
  outline: none;
}

.pokemon-btn {
  background-color: #033860;
  color: white;
  border: 1px solid white;
  border-radius: 0;
}
</style>
