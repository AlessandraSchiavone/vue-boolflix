<template>
  <div class="card" >
     <img class="poster"  v-if="item.poster_path != null" :src="url + item.poster_path" :alt="item.original_title">
     <img class="poster" v-else src="../assets/bcknet.jpg" alt="">
     <div class="card-info">
         <div class="text"> <span> Titolo: </span> {{ item.name}} </div>
        <div class="text"><span> Titolo Originale: </span> {{ item.original_name}} </div>
        <div class="text" v-if="item.original_language == stringen"><span> Lingua: </span> 
                <img class="band" src="../assets/en.png" alt=""> </div>
        <div class="text" v-else-if="item.original_language == stringit"><span> Lingua: </span> 
                <img class="band" src="../assets/it.png" alt=""> </div>
        <div class="text" v-else><span> Lingua: </span> {{item.original_language}}</div>                   
        <div class="text"><span> Voto: </span> {{ Math.round(item.vote_average / 2) }} </div>
        <div id="overvw" class="text" v-if="item.overview.length != 0 " ><span> Overview: </span> {{ item.overview.substring(0,250) + "..." }}</div>
     </div>  
  </div>
</template>

<script>
export default {
     name:"CardSerie",
     props: [ "item" ],
     data: function() {
        return {
            stringen: 'en',
            stringit: 'it',
            url:'https://image.tmdb.org/t/p/w342',
        }
    }

}
</script>

<style lang="scss" scoped>
.card{
    position:relative;
    height:100%;
    cursor:pointer;
    .poster{
        width:100%;
        height:100%;
    }
    &:hover .card-info{
        display:block;
    }
    .card-info{
        display:none;
        position:absolute;
        top:0;
        height:100%;
        width:100%;
        padding:15px;
        color:white;
        background-color: rgba(black,0.8);
        .text span{
            color:rgba(red,0.4);
            font-style: italic;
            font-weight: 700;
        }
        #overvw{
        font-size:14px;
    }
    }
}
    
</style>