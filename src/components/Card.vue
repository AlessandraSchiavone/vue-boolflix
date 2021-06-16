<template>
  <div class="card">
       <img class="poster" v-if="item.poster_path != null " :src="url + item.poster_path" >
       <img class="poster" v-else src="../assets/bcknet.jpg" alt="">
       <div class="card-info">
            <div class="text"><span> {{ item.title ? item.title : item.name}} </span>  </div>
            <div class="text"><span> Titolo Originale: </span> {{ item.original_title ? item.original_title : item.original_name}} </div>
            <div class="text" v-if="availableFlags.includes(item.original_language)">
                <span> Lingua: </span>
                <img 
                class="band"
                :src="require(`../assets/${item.original_language}.png`)"
                :alt="`bandiera ${item.original_language} `"
                >
            </div>
            <div v-else class="text"><span> Lingua: </span> {{item.original_language}}</div> 
            <div class="text"><span> Voto:  </span>
                <span>
                <i 
                v-for="index in starFull(item)"
                :key="index"
                class="fas fa-star"></i>
                    </span>
                <span>
                <i 
                v-for="index in (5 - starFull(item))"
                :key="index"
                class="far fa-star"></i>
                </span>
            </div>
            <div class="text" v-if="actors.length != 0">
                <span>Cast:</span>
                <ol class="cast">
                    <li v-for="(actor, index) in actors" :key="index">
						{{ actor.name }}</li>
                </ol>
                
            </div>
            <div id="overvw" class=" text" v-if="item.overview.length != 0 " ><span> Overview: </span> {{ item.overview.substring(0,300) + "..." }}</div>
        </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
     name:"Card",
     props: [ "item" ],
     data: function() {
        return {
            availableFlags:['it', 'en'],
            film:this.item,
            serie:this.item,
            actors:[],
            urlActorsMovie:'https://api.themoviedb.org/3/movie',
            url:'https://image.tmdb.org/t/p/w342',
        }
    },
    methods:{
        starFull: function(obj) {
                const starfull = Math.round(obj.vote_average / 2);
               return starfull;         
        },
        searchActors: function(){
            
        },
        getUrl() {
			return `${this.urlActorsMovie}/${this.film.id.toString()}/credits`;
		}
    },
    created() {
        axios.get(this.getUrl(), {
                    params:{
                        api_key: "c6d669c444d3c26032b4f5caf73674ad",
                        language: "it-IT"
                    }
                })
                .then(
                    (response) => {
                            const lunghezza = 5; 
                            for(let i=0; i< lunghezza;i++){
                                if(response.data.cast[i] != undefined){
                                    this.actors.push(response.data.cast[i]);
                                }   
                            }        
                    }
                    )
        .catch();
        
    }
}
</script>

<style lang="scss" scoped>
@import '../style/mixin';
.card{
    @include card;
}    
.band{
    height:15px;
}
.cast{
    font-size:12px;
}
</style>