<template>
  <div>
      <Search @performSearch="search" />
      <div class="container" v-if="!loading ">
        <div id="films" v-if="films.length != 0">
            <h1>Film</h1>
            <div   
                class="col-card" 
                v-for="film,index in films"
                :key="index"    
                >
                <CardFilm 
                    :item="film"
                />
               
            </div>
        </div>
        
        <div id="series" v-if="series.length != 0">
            <h1>Serie Tv</h1>
                <div 
                    class="col-card"
                    v-for="serie,index in series"
                    :key="index"    
                    >
               
                <CardSerie 
                    :item="serie"
                />
                </div>
        </div>
        
        <div
            class="neg-response"
            v-else-if="films.length == 0  || series.length == 0"
        >
            <!-- <Error /> -->
            <h1>{{ msg }}</h1>
        </div>
        </div>
        <Loader v-else />
  </div>
</template>

<script>
import Search from './Search';
import Loader from './Loader';
import CardFilm from './CardFilm.vue';
import CardSerie from './CardSerie.vue';
// import Error from './Error';
import axios from 'axios';
export default {
 name: "FilmList",
    components: {
        Search,
        Loader,
        CardFilm,
        CardSerie
        // Error
    },
    data: function() {
        return {
            films: [],
            series:[],
            loading: true,
            searchFieldText: '',
            msg: '',
            
        }
    },
    methods: {
        search: function(text) {
            this.searchFieldText = text;
            axios
                .get('https://api.themoviedb.org/3/search/movie', {
                    params:{
                        api_key: "c6d669c444d3c26032b4f5caf73674ad",
                        query: this.searchFieldText,
                        language: "it-IT"
                    }
                })
                .then(
                    (response) => {
                            this.films = response.data.results;
                            if(this.films.length == 0){
                                this.msg = "Nessun risultato per la ricerca " + this.searchFieldText;
                            }
                            this.loading = false;     
                    }
                    )
                .catch();
            axios
                .get('https://api.themoviedb.org/3/search/tv', {
                    params:{
                        api_key: "c6d669c444d3c26032b4f5caf73674ad",
                        query: this.searchFieldText,
                        language: "it-IT"
                    }
                })
                .then(
                    (response) => {
                        this.series = response.data.results;
                        if(this.series.length == 0){
                            this.msg = "Nessun risultato per la ricerca " + this.searchFieldText;
                        }
                        this.loading = false;
                    }
                    )
                .catch();
        },
    }
}
    
    
</script>

<style lang="scss" >
#films,
#series{
    display: flex;
    flex-wrap: wrap;
    h1{
        width:100%;
        text-transform: uppercase;
        font-weight: 600;
        font-style: italic;
        color:white;
        padding:10px;
    }
    .col-card{ 
        width:calc(100% / 6 - 20px);
        margin-right:20px;
        margin-bottom:20px;
        height:500px;
    }
    .text{
        color:white;
        font-size: 20px;
        padding:5px;
        .band{
            height:15px;
        }
    }  
   
}
.neg-response{
    height:calc(100vh - 80px);
    
    h1{
        
        display: inline;
        padding:10px;
        color:white;
        font-size: 25px;
    }
}
</style>