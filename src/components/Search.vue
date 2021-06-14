<template>
  <div class="search-bar">
    <img src="../assets/Logo.png" alt="">
    <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model.trim="searchText"
           
            >
            <!--@keyup="$emit('performSearch', searchText)" -->
     <div > 
          <button
            type="submit"
            class="btn"
            @click.prevent="$emit('performSearch', searchText)"
            >
                Cerca
            </button>
      </div>
  </div>
</template>

<script>
// import axios from 'axios';
export default {
    name:"Search",
    data:
    function() {
        return {
            searchText: '',
        }
    },
}
</script>

<style lang="scss" scoped>
.search-bar{
    height:80px;
    background-color:black ;
    img{
      padding:10px;
      height:100%;
    }
    .form-control{
      position: absolute;
      padding:10px;
      top:20px;
      right:80px;
    }
    .btn{
      position: absolute;
      padding:3px;
      top:28px;
      right:20px;
    }
}
</style>