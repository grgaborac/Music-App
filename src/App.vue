<template>
  <h1>Vue 3 Music App</h1>

  <MusicApp />
</template>

<script>
import MusicApp from './components/MusicApp.vue';
export default {
  name: 'App',
  components: {
    MusicApp
},
  data: function() {
    return {
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

h1{
  margin-bottom: 50px;
}
</style>