<template>
  <div>
    <header class="main-header">
      <router-link to="/">
        <h1>Vue - Pokedex</h1>
      </router-link>
      <router-link to="/user">PROFILE</router-link>
    </header>
    <router-view :pokemons="pokemons" @remove="removePokemon" @save="savePokemon"/>
  </div>  
</template>

<script>

export default {
  data() {
        return {
            pokemons: [],
        };
    },
    created() { // Component Lyfecycle Diagram https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram
        fetch('https://api.jsonbin.io/b/5ab37f77989617146bd6eb29') 
            .then(response => response.json())
            .then(pokemons => this.pokemons = pokemons);
    },
    methods: {
        removePokemon(pokemonToDelete) {
            this.pokemons = this.pokemons
                .filter(pokemon => pokemon !== pokemonToDelete);
        },
        savePokemon(pokemonToUpdate){
          this.pokemons.splice(this.pokemons.findIndex(pokemon => pokemon.id ===pokemonToUpdate.id), 1, pokemonToUpdate);
        }
    }
}
</script>

<style lang="scss">
.main-header {
    text-transform: uppercase;
    background: #42b883;
    color: white;
    //font-size: 35px;
    padding: 0.5em;
    font-weight: 400;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-right: 25px
}
a {
      text-decoration: none;
      color: white;
    }
</style>
