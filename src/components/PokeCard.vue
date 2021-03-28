<template>
  <div class="post">
    <div v-if="loading" class="loading">
      Loading...
    </div>

    <div v-if="error" class="error">
      {{ error }}
    </div>
      <div v-if="singlePokemon" class="pokeCard">
        <img @click="flipCard" v-if="front === false" class="pokeImg" :src="singlePokemon.sprites.front_default" alt="Image"  />
        <img @click="flipCard" v-if="front === true" class="pokeImg" :src="singlePokemon.sprites.back_default" alt="Image"  />
        <div >
          <input  type="radio" id="dewey" name="drone" :checked="front === false">
          <input type="radio" id="dewey" name="drone" :checked="front === true" >
        </div>
        <!-- <div v-if="front === false">
          <input type="radio" id="dewey" name="drone" >
          <input type="radio" id="dewey" name="drone" checked>

        </div> -->
        <h2>{{singlePokemon.name.charAt(0).toUpperCase() + singlePokemon.name.slice(1)}}</h2>
        <div class="cardbody">
          <!-- Types Div  -->
          <div>
            <div>
              <h4>Type:</h4>
              <div class="typeholder">
                  <h5 v-for="(type, index) in singlePokemon.types" :key="index"> <span>| {{type.type.name}} | </span></h5>
              </div>

            </div>
            <h4>Locations Found In:</h4>
            <div v-if="encounters.length > 0" class="encountersBox">

              <h5  v-for="(el, index) in encounters" :key="index"> <span>{{el.location_area.name}} </span></h5>
            </div>

          </div>
          <!-- Stats Div -->
          <div>
            <h4>Stats:</h4>
            <h5 v-for="(stat, index) in singlePokemon.stats" :key="index"> {{stat.stat.name}} :<span> {{stat.base_stat}} </span></h5>
          </div>
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
    error:null,
    encounters:'',
    front:true,
    image:'',
    imageFront:'',
    imageBack:''
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
mounted(){
  this.flipCard()
},
methods:{
  fetchData () {
        this.error = this.post = null
        this.loading = true
        const fetchedId = this.$route.params.id

        axios.get(`https://pokeapi.co/api/v2/pokemon/${fetchedId}`)
          .then(response => {
            this.singlePokemon = response.data
            // this.imageFront = response.data.sprites.front_default
            // this.imageBack = response.data.sprites.back
            this.loading = false
            console.log(this.singlePokemon)
          })
          .then(response => {
            console.log(response)
            return axios.get(`https://pokeapi.co/api/v2/pokemon/${fetchedId}/encounters`)
          .then(response =>{
            this.encounters = response.data
            console.log('this is encounters:', this.encounters)
          } )
          })
          .catch(error => this.error = error)



      },
      flipCard(){
        this.front = !this.front
        console.log(this.front)
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
.cardbody {
  display: flex;
  flex-direction: row;
  justify-content: space-around;

}

.pokeImg {
  width:200px;
  height:200px;
  border:4px solid red;
  border-radius: 20px;
  margin-top:20px;
}

.encountersBox{
  overflow: scroll;
  height:100px;
  overflow-x: hidden;
}

h4 {
  text-decoration: underline;
  font-weight: 800;
}

.typeholder {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
span {

}
</style>
