<template>
  <div>
      <Header/>
      <div class="big-cont">
      <Aside @performSearch="search" />
      <div class="container-full" v-if="!searchInit ">
        <div id="films">
            <h1>Film</h1>
                <Select @performSelectGenre="selectGenerFilm" :genresTypes="filmsGenres"/>
                <Card
                    class="col-card"
                    v-for="film,index in filteredFilm()"
                    :key="index"
                    :item="film"
                    :genresTypes="filmsGenres"  
                />
        </div>

        <div id="series" >
            <h1>Serie Tv</h1> 
                <Select @performSelectGenre="selectGenerSerie" :genresTypes="seriesGenres"/>
                <Card
                    class="col-card"
                    v-for="serie,index in filteredSerie()"
                    :key="index"
                    :item="serie"
                    :genresTypes="seriesGenres"
                />
        </div>

        <div
            class="neg-response"
            v-if="filteredFilm().length == 0  && filteredSerie().length == 0"
        >
            <!-- <Error /> -->
            <h1>{{ msg }}</h1>
        </div>
      </div>
      <Home v-else />
       </div>
  </div>


</template>

<script>
import Header from './Header';
import Aside from './Aside';
import Home from './Home';
import Card from './Card';
import Select from './Select';
import axios from 'axios';
export default {
 name: "FilmList",
    components: {
        Header,
        Aside,
        Home,
        Card,
        Select
    },
    data: function() {
        return {
            films: [],
            series:[],
            searchInit: true,
            searchFieldText: '',
            msg: '',
            selectFieldGenrFilm: '',
            selectFieldGenrSerie: '',
            filmsGenres: [],
			seriesGenres: []
        }
    },
    methods: {
        search: function(text) {
            this.searchFieldText = text;
            /*Chiamata per film*/
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
                            this.searchInit = false;     
                    }
                    )
                .catch();
            /*Chiamata per Serie*/
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
                        this.searchInit = false;
                    }
                    )
                .catch();
        
        },
        selectGenerFilm: function(text){
            this.selectFieldGenrFilm = text;
        },
        selectGenerSerie: function(text){
            this.selectFieldGenrSerie = text;
        },
        filteredFilm: function(){
            var filteredArray = [];
            if(this.selectFieldGenrFilm == "" || this.selectFieldGenrFilm == "All"){
                return this.films;
                }else {
                    filteredArray = this.films.filter((element) => {
					return element.genre_ids.toString().includes(
						this.selectFieldGenrFilm
					);
				});
            return filteredArray;
                }
             },   
        filteredSerie: function(){
            var filteredArray = [];
            if(this.selectFieldGenrSerie == "" || this.selectFieldGenrSerie == "All"){
                return this.series;
                }else {
                    filteredArray = this.series.filter((element) => {
					return element.genre_ids.toString().includes(
						this.selectFieldGenrSerie
					);
				});
             return filteredArray;
                }
             },
    },
    created() {
        axios.get("https://api.themoviedb.org/3/genre/movie/list", {
                    params:{
                        api_key: "c6d669c444d3c26032b4f5caf73674ad",
                        language: "it-IT"
                    }
                })
                .then(
                    (response) => {
                        this.filmsGenres = response.data.genres;        
                    }
                    )
        .catch();
        axios.get("https://api.themoviedb.org/3/genre/tv/list", {
                    params:{
                        api_key: "c6d669c444d3c26032b4f5caf73674ad",
                        language: "it-IT"
                    }
                })
                .then(
                    (response) => {
                        this.seriesGenres = response.data.genres;        
                    }
                    )
        .catch();
    }
}
</script>

<style lang="scss" >
.big-cont{
    display:flex;
}
#films,
#series{
    position:relative;
    display: flex;
    flex-wrap: wrap;
    h1{
        width:100%;
        font-weight: 600;
        color:white;
        padding:10px;
    }
    .col-card{
        width:calc(360px - 20px);
        margin:10px;
        height:560px;
    }
}
.neg-response{
    height:calc(100vh - 80px);
    h1{
        padding:10px;
        color:white;
        font-size: 25px;
    }
}
</style>