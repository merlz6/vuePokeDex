<template>
  <div class="home">
    <h1>Welcome to the VueDex</h1>
    <img alt="PokeBall" class="pokeballHomePic" src="https://poketouch.files.wordpress.com/2020/11/die_cast_poke_ball_replica.jpg">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {

  }
}
</script>
<style scoped>

.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

  .pokeballHomePic{
    width:50%;
    height:50%;
    border-radius: 10px;
    margin: 50px auto;
  }

</style>
