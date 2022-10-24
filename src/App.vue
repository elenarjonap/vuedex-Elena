<template>
  <header class="header">
    <div>
      Type Pokemon or ID:
      <input type="text" v-model="pokemonID"> 
      <button class="clickbutton" @click="searchPokemon">Search Pokemon</button>
    </div>

    <body class="body">
      <section class="pokemonCard" v-for="pokemon in pokemonData">
        <PokeCard
              :pokemon="pokemon"
              @remove="removePokemon"
            />
      </section>

    </body>
   

  </header>
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
  },
  watch: {},
  computed: {},
  mounted() { }
}
</script>


<style scoped>

</style>
