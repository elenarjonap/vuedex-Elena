<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12 text-center">
        <h1 class="title my-4">Pokédex</h1>
      </div>
    </div>

    <div class="row">
      <div class="form-group mb-2 mr-2">
        <input type="text" class="form-control" id="name" placeholder='Introduce el id o nombre del pokemon' v-model="pokemonID">
      </div>
      <button class="btn btn-secondary mb-2" @click="searchPokemon">Buscar</button>
    </div>
  
    <div class="col-md-12">
      <div class="row card-container">
        <div class="card-item col-md-3 text-center" v-for="pokemon in pokemonData">
          <PokeCard
            :pokemon="pokemon"
            @remove="removePokemon"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PokeCard from  './components/PokeCard.vue'

export default {
  name: "Vuedex",
  components: {
    PokeCard
  },
  data() { return {
    pokemonData: [],
    pokemonID: "",
  } },
  methods: {
    async searchPokemon (){
      try {
        const pokemonFind = await fetch ('https://pokeapi.co/api/v2/pokemon/' + this.pokemonID)
        const pokemon = await pokemonFind.json()
        let currentDate = new Date()
        pokemon.internalId = currentDate.getTime()
        this.pokemonData.push(pokemon)
        console.log(typeof pokemon)
        console.log(pokemon)
        return pokemon

      }catch (error){
        alert ("It's not a Pokemon")

      }
    },
    removePokemon(internalId) {
      console.log(internalId) 
      this.pokemonData = this.pokemonData.filter((pokemon) => pokemon.internalId !== internalId)
    }
  }
}
</script>
