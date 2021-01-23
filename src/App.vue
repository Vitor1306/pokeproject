<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
            <img src="./assets/pokelogo.png">
            <hr>
            <h4 class="is-size-4">Pokedex</h4>
            <input type="text" name="" id="" placeholder="Gotta catch em' all!" v-model="search" class="input is-rounded">
            <hr>
              <button class="button is-success">Search!</button>

      <div v-for="(poke,index) in SearchResult" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/> 
      </div>      
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      search: ''
    }
  },
    created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log("Gotcha");
      this.pokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  computed: {
    SearchResult: function(){
      if(this.search == '' || this.search == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.search);
      
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
</style>