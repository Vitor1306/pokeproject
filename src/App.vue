<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
            <img src="./assets/pokelogov2.png">
            <hr>
            <h4 class="is-size-4">Pokedex</h4>
            <input type="text" name="" id="" placeholder="Gotta catch em' all!" v-model="search" class="input is-rounded">
            <hr>
              <button class="button is-success" @click="bsearch">Search!</button>

      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
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
      filteredPokemons: [],
      search: ''
    }
  },
    created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log("Gotcha");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  methods:{
    bsearch: function(){
      if(this.search == '' || this.search == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search)
      }
    }  
  },
  
  computed: {
    /*
    SearchResult: function(){
      if(this.search == '' || this.search == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.search);
      
    }
  }
  */
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

  background :url(./assets/pokeback.png) no-repeat center top fixed;
 

-webkit-background-size: cover; -moz-background-size: cover; -o-background-size: cover; background-size: cover;
}
</style>