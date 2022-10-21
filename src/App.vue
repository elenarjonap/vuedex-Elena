<template>
  <header class="header">
    <div>
      Type Pokemon or ID:
      <input type="text" v-model="pokemonID"> 
      <button class="clickbutton" @click="searchPokemon">Search Pokemon</button>
    </div>

    <body class="body">
      <section class="pokemonCard" v-for="pokemon in pokemonData">
        <div class="pokemon">
          <h1 class="pokemonName">{{pokemon.name}}</h1>
          <img :src="pokemon.sprites.front_default" alt="pokemon.name">
        </div>

        <ul class="type">
          <h2>Types</h2>
          <li v-for="type in pokemon.types">{{type.type.name}}</li>
        </ul>

      </section>

    </body>
   

  </header>
</template>

<script>
export default {
  name: "Vuedex",
  data() { return {
    pokemonData: [],
    pokemonID: "",
  } },
  methods: {
    async searchPokemon (){
      try {
        const pokemonFind = await fetch ('https://pokeapi.co/api/v2/pokemon/' + this.pokemonID)
        const pokemon = await pokemonFind.json()
        this.pokemonData.push(pokemon)
        console.log(pokemon)
        return pokemon

      }catch (error){
        alert ("It's not a Pokemon")

      }
    }
  },
  watch: {},
  computed: {},
  mounted() { }
}
</script>


<style scoped>

</style>
