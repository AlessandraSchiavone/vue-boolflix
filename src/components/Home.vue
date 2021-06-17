<template>
  <div class="home-container">
      <div class="home-text">
          <h3>Film, serie TV e tanto altro. Senza limiti.</h3>
          <h6>Guarda ciò che vuoi ovunque. Disdici quando vuoi.</h6>
      </div>
  </div>
</template>

<script>
export default {
 name:"Home"
}
</script>

<style lang="scss" scoped>
.home-container{
    position:relative;
    background-image: url("../assets/box.jpg");
    width:calc(100% - 50px);
    height:calc(100vh - 80px);
    background-size: cover;
    .home-text{    
        position:absolute;
        top:50%;
        left:50%;
        transform: translate(-50%,-50%);
        text-align: center;
        color:white;
        h3{
            font-size: 80px;
            font-weight: 700;
        }
        h6{
            font-size: 30px;
        }
    }
}
</style>