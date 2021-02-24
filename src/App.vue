<template>
  <b-container id="app" class="mt-2" fluid>
    <b-row>
        <b-col v-for="(pokemon, index) in pokemonList" :key="index" class="mb-2">
            <Poke :name="pokemon.name" :url="pokemon.url" :index="index+1"/>
        </b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from 'axios';
import Poke from './components/Poke'

export default {
    data(){
        return{
            pokemonList: [],
            pokemonURLS: []
        }
    },
    created: function(){
        axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=> {
            this.pokemonList = res.data.results;
        })
    },
    components:{
      Poke
    }
}
</script>

<style>

body{
  background: tomato;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
