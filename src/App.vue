<template>
  <div id="app">
    <img class="logo" src="./assets/pokemon-logo.png" />
    <Pokeguia />
  </div>
</template>

<script>
import Pokeguia from "./components/Pokeguia.vue";
export default {
  name: "App",
  components: {
    Pokeguia,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-image: url("https://assets.pokemon.com//assets/cms2-es-es/img/misc/virtual-backgrounds/sword-shield/pokemon-in-the-wild.png");
  background-repeat: no-repeat;
  background-size: cover;
}
.logo {
  width: 50vh;
}
</style>
