<template>
  <div id="app">
    <b-container class="mt-2">
      <b-row>
        <Poke/>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Poke from './components/Poke'

export default {
  name: 'App',
  data(){
    return {
      
    }
  },
  components: {
    Poke
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
