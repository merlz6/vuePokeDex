<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
          <router-link to="/about">About</router-link> |
            <!-- <router-link :to="{name:'AnotherView', query:{hello:this.hello}}" >AnotherView</router-link> -->
            <div v-for="(poke, index) in pokemon" :key='index'>
                  <router-link :to="{ name: 'PokeCard', params: {name:poke.name}}">{{poke.name}}</router-link>
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
    .get('https://pokeapi.co/api/v2/pokemon')
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
  flex-direction: row;
  justify-content: space-around;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
