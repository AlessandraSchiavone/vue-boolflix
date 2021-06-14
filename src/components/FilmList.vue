<template>
  <div >
      <Search @performSearch="search" />
      <div class="container" v-if="!loading ">
        <div id="films" v-if="films.length != 0">
            <h1>Film</h1>
            <div    
                class="films col-card"
                v-for="film,item in films"
                :key="item"    
                >
                <div class="text">Titolo: {{ film.title}} </div>
                <div class="text">Titolo Originale: {{ film.original_title}} </div>
                <div class="text" v-if="film.original_language == stringen">Lingua: 
                    <img src="../assets/en.png" alt=""> </div>
                <div class="text" v-else-if="film.original_language == stringit">Lingua: 
                    <img src="../assets/it.png" alt=""> </div>
                    <div class="text" v-else>Lingua: {{film.original_language}}</div>
                    
                <div class="text">Voto: {{ film.vote_average}} </div>
            </div>
        </div>
        
        <div id="series" v-if="series.length != 0">
            <h1>Serie Tv</h1>
                <div 
                    class="col-card"
                    v-for="serie,item in series"
                    :key="item"    
                    >
                <div class="text">Titolo: {{ serie.name}} </div>
                    <div class="text">Titolo Originale: {{ serie.original_name}} </div>
                    <div class="text" v-if="serie.original_language == stringen">Lingua: 
                        <img src="../assets/en.png" alt=""> </div>
                    <div class="text" v-else-if="serie.original_language == stringit">Lingua: 
                        <img src="../assets/it.png" alt=""> </div>
                        <div class="text" v-else>Lingua: {{serie.original_language}}</div>
                                
                    <div class="text">Voto: {{ serie.vote_average}} </div>
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
// import Error from './Error';
import axios from 'axios';
export default {
 name: "FilmList",
    components: {
        Search,
        Loader,
        // Error
    },
    data: function() {
        return {
            films: [],
            series:[],
            loading: true,
            searchFieldText: '',
            msg: '',
            stringen: 'en',
            stringit: 'it',

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
                        console.log(this.films)
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
                        console.log(this.series)
                    }
                    )
                .catch();
        },
    }
}
    
    
</script>

<style lang="scss" scoped>

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
        width:calc(100% / 6 - 10px);
        height:500px;
        margin-right:10px;
        margin-bottom:10px;
        background-color: rgb(31, 31, 31);
        
    }

    .text{
            padding:10px 20px;
            color:white;
            font-size: 30px;
            img{
                height:20px;
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