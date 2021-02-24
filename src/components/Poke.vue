<template>
    <b-card>
        <template #header> #{{index}} - {{ name | Capitalizer }} </template>
        <b-row>
            <b-col cols="5" class="ml-auto">
                <b-button class="flip-btn" @click="flipSprite()">Mudar sprite</b-button>
            </b-col>
        </b-row>
        <b-card-img :src="currentImg" alt="Pokemon image" @mouseover="flipSprite()" @mouseleave="flipSprite()"></b-card-img>
        <b-card-sub-title class="pokemon-types">
            <b-row>
                <b-col v-for="(types, typesIndex) in pkmnTypes" :key="typesIndex">
                    <p :class="types.type.name"><b>{{types.type.name | Capitalizer}}</b></p>
                </b-col>
            </b-row>
        </b-card-sub-title>
        <b-list-group>
            <p class="mt-3"><b>HABILIDADES:</b></p>
            <b-list-group-item v-for="(abilities, abilityIndex) in pkmnAbilities" :key="abilityIndex">
                {{abilities.ability.name | Capitalizer}}
            </b-list-group-item>
        </b-list-group>
    </b-card>
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return{
            pkmnTypes: [],
            pkmnAbilities: [],
            isFront: true,
            currentImg: '',
            pkmnFrontSprites: '',
            pkmnBackSprites: '',
        }
    },
    props:{
        name: String,
        url: String,
        index: Number
    },
    created: function (){
        axios.get(this.url).then(res=> {
            this.pkmnFrontSprites = res.data.sprites.front_default
            this.pkmnBackSprites = res.data.sprites.back_default
            this.pkmnTypes = res.data.types
            this.pkmnAbilities = res.data.abilities
            this.currentImg = this.pkmnFrontSprites
        });
    },
    filters:{
        Capitalizer: function(value){
            return value.charAt(0).toUpperCase()+value.slice(1) //Capitalize it
        }
    },
    methods: { 
        flipSprite: function(){
            if (this.isFront == true) {
                this.currentImg = this.pkmnBackSprites
                this.isFront = false
                console.log('Trocar para back')
            } else{
                this.currentImg = this.pkmnFrontSprites
                this.isFront = true
                console.log('Trocar para front')
            }
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Staatliches&display=swap');

.card{
    max-width: 250px;
    min-width: 250px;
}

.flip-btn{
    background: silver;
    border: 0px;
    font-size: 12px;
    width: 65px;
}

.pokemon-types{
    font-family: 'Staatliches', cursive;
    background: gainsboro;
    border-radius: 2%;
    padding-left: 10px;
    padding-top: 10px;
    font-size: 18px;
}

.normal{
    -webkit-text-stroke: 0.3px gray;
    -webkit-text-fill-color: beige;
}
.grass{
    color:forestgreen;
}
.poison{
    color: purple;
}
.fire{
    color: orangered;
}
.flying{
    -webkit-text-stroke: 0.3px gray;
    -webkit-text-fill-color: lightcyan;
}
.water{
    color: dodgerblue;
}
.bug{
    color:darkgreen;
}
.electric{
    -webkit-text-stroke: 0.3px gray;
    -webkit-text-fill-color: yellow;
}
.ground{
    color:chocolate;
}
.fairy{
    -webkit-text-stroke: 0.3px gray;
    -webkit-text-fill-color: white;
}
.psychic{
    color: palevioletred;
}
.fighting{
    color: brown;
}
.rock{
    color: gray;
}
.ghost{
    color:blueviolet;
}
</style>