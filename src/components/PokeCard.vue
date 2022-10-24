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
  <div class="card-box">
    <a class="remove-btn" href="#" @click="emitRemove">X</a>
    <img class="photo" :src="pokemon.sprites.front_default" :alt="pokemon.name" />
    <h2 class="name mb-2">{{pokemon.name}}</h2>
    <ul class="type-list">
      <li class="type-item" v-for="type in pokemon.types">{{type.type.name}}</li>
    </ul>
  </div>
</template>
