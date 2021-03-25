<template>
  <div id="app">
    <div id="nav">
          <h2 class="navbarh2">Pokemon</h2>
            <!-- <router-link :to="{name:'AnotherView', query:{hello:this.hello}}" >AnotherView</router-link> -->
            <div v-for="(poke, index) in pokemon" :key='index'>
                  <router-link :to="{ name: 'PokeCard', params: {id:index +1}}">{{poke.name}}</router-link>
            </div>

    </div>
    <router-view/>
    <!-- {{pokemon}} -->

  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {

  },
  data:function(){
    return {
      pokemon:[null]
    }
  },
  mounted(){
    axios
    .get('https://pokeapi.co/api/v2/pokemon?limit=1118')
    .then(response => (this.pokemon = response.data.results))
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  /* flex-direction: row;
  justify-content: space-around; */
  grid-template-columns: 1fr 2fr;
  grid-template-rows: 1fr;
  border: 5px solid white;
  border-radius: 10px;
  height:600px;
}
body {
  background-color: red;
}
#nav {
  padding: 20px;
  width:25%;
  border: 2.5px solid black;
  max-height:580px;
    overflow: scroll;
}

.post {
  width:70%;
  background-color: ghostWhite;
  border: 2.5px solid black;
  max-height:600px;
}

#nav a {
  font-weight: bold;
  color: ghostWhite;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.navbarh2 {
  text-decoration: underline;
}
</style>
