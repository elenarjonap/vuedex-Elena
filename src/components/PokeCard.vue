<script>
export default { 
  props: {
    pokemon: Object
  },
  emits: ['remove'],
  methods: {
    emitRemove() {
      this.$emit('remove', this.pokemon.internalId)
    }
  }
}
</script>

<template>
  <div class="pokemon">
    <a class="remove-btn" href="#" @click="emitRemove">X</a>
    <h1 class="pokemonName">{{pokemon.name}}</h1>
    <img :src="pokemon.sprites.front_default" alt="pokemon.name">
  </div>

  <ul class="type">
    <h2>Types</h2>
    <li v-for="type in pokemon.types">{{type.type.name}}</li>
  </ul>
</template>
