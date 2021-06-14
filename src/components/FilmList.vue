<template>
  <div >
      <Search @performSearch="searchFilm" />
      <div class="container" v-if="!loading ">
        <div 
                class="col-card"
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
                
                <!-- <Character
                    :item="character"
                /> -->
        </div>
        <div
            class="neg-response"
            v-if="films.length == 0"
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
            loading: true,
            searchFieldText: '',
            msg: '',
            stringen: 'en',
            stringit: 'it',

        }
    },
    methods: {
        searchFilm: function(text) {
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
                            this.msg = "Non ci sono film da visualizzare"
                        }
                        this.loading = false;
                        console.log(this.films)
                    }
                    )
                .catch();
        }
    }
}
    
    
</script>

<style lang="scss" scoped>

.container{
    // max-width:1470px;
    // margin:0 auto;
    // height:calc(100% - 80px);
    display: flex;
    flex-wrap: wrap;
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