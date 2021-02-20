<template>
    <div>
        <b-col v-for="(pokemon, index) in pokemonList" :key="index">
            <b-card>
                <b-card-title>{{ pokemon.name | pkmnNameCapitalizer }}</b-card-title>
                <b-card-body>{{ pokemon.url }}</b-card-body>
            </b-card>
        </b-col>
    </div>
</template>

<script>
import axios from 'axios';

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
            /* console.log(res.data.results); */
        })
    },
    filters:{
        pkmnNameCapitalizer: function(value){
            return value.charAt(0).toUpperCase()+value.slice(1) //Capitalize it
        }
    },
}
</script>

<style>
.card{
    height: 180px;
    width: 300px;
}
</style>