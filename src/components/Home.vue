<template>
  <div class="box">
      <div class="init">
          <h3>Film, serie TV e tanto altro. Senza limiti.</h3>
          <h4>Guarda ciò che vuoi ovunque. Disdici quando vuoi.</h4>
      </div>
  </div>
</template>

<script>
export default {
 name:"Home"
}
</script>

<style lang="scss" scoped>
.box{
    position:relative;
    background-image: url("../assets/box.jpg");
    height:calc(100vh - 80px);
    background-size: cover;
    .init{    
        position:absolute;
        top:50%;
        left:50%;
        transform: translate(-50%,-50%);
        font-size: 55px;
        text-align: center;
        color:white;
    }
}
</style>