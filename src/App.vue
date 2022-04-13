<template>

  <div id="app">

    <div class="column is-half is-offset-one-quarter">
            <img src="../public/img/01.png" id="img_poke">
            <img  src="../public/img/02.png" id="img_poke">

            <hr>
      <input class="input is-success" type="text" placeholder="Buscar Pokemon" v-model="busca">
      <button class="button is-medium is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>

      <div v-for="(poke, index) in filterPokemons" :key="poke.url" >
        <Pokemon :name="poke.name" :url="poke.url" :num="index +1"/>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import Pokemon from './components/Pokemon'


export default {
  components: { Pokemon },
  name: 'App',
  data(){
    return{
      pokemons : [],
      filterPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res)=>{

      this.pokemons= res.data.results
      this.filterPokemons = res.data.results
    })
  },
  component: {
   Pokemon
 },
 methods:{
   buscar: function(){
     this.filterPokemons = this.pokemons
     if(this.busca == '' || this.busca ==' '){
        this.filterPokemons == this.pokemons
     }else{
       this.filterPokemons = this.pokemons.filter(pokemons => pokemons.name == this.busca)
     }
   }
 },
 computed:{
   
   resultadoBusca: function(){
     if(this.busca == '' || this.busca ==' '){
       return this.pokemons
     }else{
       return this.pokemons.filter(pokemons => pokemons.name == this.busca)
     }
   }
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
  margin-top: 60px;
 
}
#img_poke {
  margin-top: 1%;
  width: 20%;
  
}
#buscaBtn{
  margin-top: 2%;
}
</style>
