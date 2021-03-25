<template>
  <div class="post">
    <div v-if="loading" class="loading">
      Loading...
    </div>

    <div v-if="error" class="error">
      {{ error }}
    </div>
      <div v-if="singlePokemon" class="pokeCard">
        <h2>{{singlePokemon.name}}</h2>
        <img :src="singlePokemon.sprites.front_default" alt="Image"  />
        <div class="cardbody">
          <h3 v-for="type in singlePokemon.types" :key="type">Type: <span>{{type.type.name}} </span></h3>
        </div>
      </div>


  </div>

</template>

<script>
import axios from 'axios'
export default {

  name: 'PokeCard',
  props: {
    pokemon: {}
  },
  data(){
    return{
    singlePokemon:'',
    loading:false,
    error:null
  }},
  created () {
  // fetch the data when the view is created and the data is
  // already being observed
  this.fetchData()
  },
  watch: {
  // call again the method if the route changes
  '$route': 'fetchData'
},
methods:{
  fetchData () {
        this.error = this.post = null
        this.loading = true
        const fetchedId = this.$route.params.name
        // replace `getPost` with your data fetching util / API wrapper
        // axios.get(`https://pokeapi.co/api/v2/pokemon/` + fetchedId, (err, post) => {
        //   // make sure this request is the last one we did, discard otherwise
        //   if (this.$route.params.name !== fetchedId) return
        //   this.loading = false
        //   if (err) {
        //     this.error = err.toString()
        //   } else {
        //     this.singlePokemon = post
        //   }
        // })
        axios.get(`https://pokeapi.co/api/v2/pokemon/${fetchedId}`)
          .then(response => {
            this.singlePokemon = response.data
            this.loading = false
            console.log(this.singlePokemon)
          })
          .catch(error => this.error = error)
      }
}
  //  mounted(){
  //   //
  //   //   .then(response => (console.log(response)))
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
