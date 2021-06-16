<template>
  <div>
      <Header/>
      <div class="big-cont">
      <Aside @performSearch="search" />
      <div class="container-full" v-if="!searchInit ">
        <div id="films" v-if="films.length != 0">
            <h1>Film</h1>
                <Card
                    class="col-card"
                    v-for="film,index in films"
                    :key="index"
                    :item="film"
                />
        </div>

        <div id="series" v-if="series.length != 0">
            <h1>Serie Tv</h1> 
                <Card
                    class="col-card"
                    v-for="serie,index in series"
                    :key="index"
                    :item="serie"
                />
        </div>

        <div
            class="neg-response"
            v-else-if="films.length == 0  && series.length == 0"
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
import Card from './Card.vue';
// import Error from './Error';
import axios from 'axios';
export default {
 name: "FilmList",
    components: {
        Header,
        Aside,
        Home,
        Card,
        // Error
    },
    data: function() {
        return {
            films: [],
            series:[],
            searchInit: true,
            searchFieldText: '',
            msg: '',
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
        
    }
}


</script>

<style lang="scss" >
.big-cont{
    display:flex;
}
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
        margin:10px;
        height:460px;
    }
    .text{
        color:white;
        font-size: 20px;
        padding:5px;
        
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