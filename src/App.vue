<template>
<div id="app">
  <header>
    <b-navbar variant="light">
      <b-navbar-brand href="#">
        <img class="pkmnLogo" src="./assets/logo.png">
      </b-navbar-brand>
      <b-nav-form class="ml-auto">
        <b-form-input placeholder="Search for a pokemon" v-model="searched"></b-form-input>
        <b-button class="search-btn ml-2">
          <b-icon icon="search"></b-icon>
        </b-button>
      </b-nav-form>
    </b-navbar>
  </header>
  <b-container  class="mt-3" fluid>
    <b-row>
        <b-col v-for="(pokemon, index) in searchedFor" :key="index" class="mb-2">
            <Poke :name="pokemon.name" :url="pokemon.url" :index="index+1"/>
        </b-col>
    </b-row>
  </b-container>
</div>
</template>

<script>
import axios from 'axios';
import Poke from './components/Poke'

export default {
    data(){
        return{
            pokemonList: [],
            pokemonURLS: [],
            searched: ''
        }
    },
    created: function(){
        axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=> {
            this.pokemonList = res.data.results;
        })
    },
    components:{
      Poke
    },
    computed: {
      searchedFor: function() {
        if (this.searched == '' || this.searched == ' ') {
          return this.pokemonList
        } else{
          return this.pokemonList.filter(pokemon => pokemon.name == this.searched)
          /* return this.pokemonList.filter(pokemon => pokemon.name.includes(this.searched)) */
        }
      },
    }
}
</script>

<style>

body{
  background: #e39081;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.pkmnLogo{
  width: 50px;
}
.search-btn{
  background: tomato;
  border: 0px;
}
.search-btn:hover{
  background: #c4462f;
  border: 0px;
}
</style>
