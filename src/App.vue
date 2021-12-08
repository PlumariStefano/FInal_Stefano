<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron">
      <h1>Final Stefano Plumari YA2C</h1>
      <br>

      <Conversor />


    </div>

  </div>
</template>

<script>
import Conversor from './componentes/Conversor.vue'


export default {
  name: 'App',
  components: {
   Conversor
  }
}
</script>

<style>

h1 {
  color: black;
}
#app {

}
</style>
