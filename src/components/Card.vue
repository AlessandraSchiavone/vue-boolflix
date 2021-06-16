<template>
  <div class="card">
       <img class="poster" v-if="item.poster_path != null " :src="url + item.poster_path" >
       <img class="poster" v-else src="../assets/bcknet.jpg" alt="">
       <div class="card-info">
            <div><span> {{ item.title ? item.title : item.name}} </span>  </div>
            <div><span> Titolo Originale: </span> {{ item.original_title ? item.original_title : item.original_name}} </div>
            <div v-if="availableFlags.includes(item.original_language)">
                <span> Lingua: </span>
                <img 
                class="band"
                :src="require(`../assets/${item.original_language}.png`)"
                :alt="`bandiera ${item.original_language} `"
                >
            </div>
            <div v-else><span> Lingua: </span> {{item.original_language}}</div> 
            <div><span> Voto:  </span>
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
            <div v-if="actors.length != 0">
                <span>Cast:</span>
                <ol class="cast">
                    <li v-for="(actor, index) in actors" :key="index">
						{{ actor.name }}</li>
                </ol> 
            </div>
            <div v-if="genres.length != 0"> 
                <span>Genere:</span>
                <div class="genre" v-for="(genre, index) in genres" :key="index">
				{{ genre }}</div>
            </div>
            <div id="overvw" v-if="item.overview.length != 0 " ><span> Overview: </span> {{ item.overview.substring(0,200) + "..." }}</div>
        </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
     name:"Card",
     props: { 
         item:Object,
         genresTypes:Array,
         },
     data: function() {
        return {
            availableFlags:['it', 'en'],
            datas:this.item,
            actors:[],
            genres: [],
            urlActorsMovie:'https://api.themoviedb.org/3/movie',
            url:'https://image.tmdb.org/t/p/w342',
        }
    },
    methods:{
        starFull: function(obj) {
                const starfull = Math.round(obj.vote_average / 2);
               return starfull;         
        },
        getUrl() {
			return `${this.urlActorsMovie}/${this.datas.id.toString()}/credits`;
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
        this.datas.genre_ids.forEach((element) => {
			for (var i = 0; i < this.genresTypes.length; i++) {
				if (element == this.genresTypes[i].id) {
					this.genres.push(this.genresTypes[i].name);
				}
			}
		});
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
    font-size:16px;
    list-style: none;
}
.genre{
    display: inline;
}


</style>