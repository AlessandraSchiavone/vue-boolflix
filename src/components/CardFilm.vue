<template>
  <div 
   class="card"
   >
       <img class="poster" v-if="item.poster_path != null " :src="url + item.poster_path" :alt="item.original_title">
       <img class="poster" v-else src="../assets/bcknet.jpg" alt="">
       <div class="card-info">
       <div class="text"><span> Titolo: </span> {{ item.title}} </div>
        <div class="text"><span> Titolo Originale: </span> {{ item.original_title}} </div>
        <div class="text" v-if="item.original_language == stringen"><span> Lingua: </span> 
            <img class="band" src="../assets/en.png" alt=""> </div>
        <div class="text" v-else-if="item.original_language == stringit"><span> Lingua: </span> 
            <img class="band" src="../assets/it.png" alt=""> </div>
        <div class="text" v-else><span> Lingua: </span>  {{item.original_language}}</div>       
        <div class="text"><span> Voto:  </span>
        <span>
        <i 
        v-for="index in starFull()"
        :key="index"
        class="fas fa-star"></i>
            </span>
            <span>
        <i 
        v-for="index in (5 - starFull())"
        :key="index"
        class="far fa-star"></i>
            </span>
        </div>
       
        <div id="overvw" class=" text" v-if="item.overview.length != 0 " ><span> Overview: </span> {{ item.overview.substring(0,500) + "..." }}</div>
        </div>
  </div>
</template>

<script>
export default {
     name:"CardFilm",
     props: [ "item" ],
     data: function() {
        return {
            stringen: 'en',
            stringit: 'it',
            film: this.item,
            url:'https://image.tmdb.org/t/p/w342',
        }
    },
    methods:{
        starFull: function() {
                const starfull = Math.round(this.film.vote_average / 2);
               return starfull;         
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/mixin';
.card{
    @include card;
}    
</style>