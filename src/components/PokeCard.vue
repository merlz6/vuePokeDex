<template>
  <div class="hello">
    This is the PokeCard Component
    {{$route.params.name}}
  </div>
</template>

<script>
export default {
  name: 'PokeCard',
  props: {
    pokemon: {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
