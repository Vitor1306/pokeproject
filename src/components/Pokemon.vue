<template>
    <div id="pokemon">
        


        <div class="card"> 
        <div class="card-image">
            <figure>
            <img :src="pokemon.front" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{num}} - {{name | upper}}</p>
                <p class="subtitle is-6">{{ pokemon.type}}</p>
                <p class="subtitle is-6"> exp:{{pokemon.exp}}</p>
                <p class="subtitle is-6">{{pokemon.skills}}</p>
            </div>
            </div>
            <div class="content">
            </div>
  </div>
</div>
    
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.exp = res.data.base_experience;
            this.pokemon.skills = res.data.move;
        })        
    },
    data(){
        return {
            pokemon: {
                type: '',
                front: '',
                exp: '',
                skills:''

            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String,
        exp: Number,
        skills: String
    },
    filters: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.substr(1);
            return newName;
        }
    }
}
</script>

<style lang="scss" scoped>
    
#pokemon{
    
    margin-top: 5%;
    margin-bottom: 5%;
}

</style>