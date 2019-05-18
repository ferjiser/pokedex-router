<template>
    <div v-if="pokemon">
         <pokemon-card
            :pokemon="pokemon"
            :type-color="TYPE_COLOR"
        ></pokemon-card>
        <p>Name: {{pokemon.name}}</p>
        <p>Height: 
         <input v-if="isEdit" class="nice-input" type="text" :placeholder="pokemon.height" v-model="newPokemon.height">
         <span v-else>{{pokemon.height}}</span>
         </p>
        <p>Weight: 
         <input v-if="isEdit" class="nice-input" type="text" :placeholder="pokemon.weight" v-model="newPokemon.weight">
         <span v-else>{{pokemon.weight}}</span>
         </p>
         <p>Types:
              <ul>
                <li v-for="type in pokemon.types" :key="type">{{type}}</li>
            </ul>
         </p>
          <p>Abilities:
              <ul>
                <li v-for="ability in pokemon.abilities" :key="ability">{{ability}}</li>
            </ul>
         </p>
         <button v-if="!isEdit" @click="toggleEdit(pokemon)">Edit</button>
         <button v-if="isEdit" @click="toggleEdit(pokemon)">Cancel</button>
         <button v-if="isEdit" @click="save(pokemon)">Save</button>
    </div>
</template>

<script>
// @ is an alias to /src
import PokemonCard from '../components/PokemonCard'

export default {
  name: 'pokemon-detail',
  props: ['pokemons', 'name'],
  data() {
        return {
            TYPE_COLOR: {
                "grass": "#78C850",
                "poison": "#A040A0",
                "fire": "#F08030",
                "flying": "#A890F0",
                "water": "#6890F0",
                "bug": "#A8B820",
                "normal": "#A8A878",
                "electric": "#F8D030",
            },
            isEdit: false,
            newPokemon: {}
        };
    },
    computed: {
        pokemon(){
            if(!this.pokemons.length) return undefined;
            const pokemon = this.pokemons.find(pokemon => pokemon.name === this.name);
                return {
                    ...pokemon,
                    image: pokemon.image.startsWith('/') ? pokemon.image : '/'+pokemon.image
                }
        }
    },
    methods: {
        toggleEdit(pokemon){
            this.isEdit = !this.isEdit;
            this.newPokemon = pokemon
        },
        save(pokemon){
            this.isEdit = false;
            this.$emit('save', this.newPokemon);
        }
    },
    components: {
        PokemonCard
    }
}
</script>
