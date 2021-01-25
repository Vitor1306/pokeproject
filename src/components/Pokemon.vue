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
    
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	grid-template-rows: repeat(2, 100px);
}

.start {
	align-items: start;
}

.end {
	align-items: end;
}

.center {
	align-items: center;
}

.stretch {
	align-items: stretch;
}

.item-2, .item-3 {
	grid-row: span 2;
}

.item-5 {
	grid-column: span 2;
}

/* Grid Item */
.item {
	margin: 5px;
	background: tomato;
	text-align: center;
	font-size: 1.5em;
}

.grid {
	max-width: 400px;
	margin: 0 auto;
	border: 1px solid #ccc;
}

h1 {
	text-align: center;
	font-size: 1.25em;
	font-weight: normal;
}

body {
	font-family: monospace;
	color: #333;
	padding-bottom: 60px;
	margin: 0px;
}

body > div {
	padding: 40px 0;
}

body > div:nth-of-type(even) {
	background: rgba(0,0,0,.03);
}

body > div > img {
	display: block;
	margin: 0 auto;
	max-width: 100%;
}

</style>