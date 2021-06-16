<template>
  <div class="card">
       <img class="poster" v-if="item.poster_path != null " :src="url + item.poster_path" >
       <img class="poster" v-else src="../assets/bcknet.jpg" alt="">
       <div class="card-info">
            <div class="text"><span> Titolo: </span> {{ item.title ? item.title : item.name}} </div>
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
            <div id="overvw" class=" text" v-if="item.overview.length != 0 " ><span> Overview: </span> {{ item.overview.substring(0,300) + "..." }}</div>
        </div>
  </div>
</template>

<script>
// import axios from 'axios';
export default {
     name:"Card",
     props: [ "item" ],
     data: function() {
        return {
            availableFlags:['it', 'en'],
            film:this.item,
            serie:this.item,
            url:'https://image.tmdb.org/t/p/w342',
        }
    },
    methods:{
        starFull: function(obj) {
                const starfull = Math.round(obj.vote_average / 2);
               return starfull;         
        },
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
</style>