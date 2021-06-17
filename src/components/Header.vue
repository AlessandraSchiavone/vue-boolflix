<template>
  <header>
    <img src="../assets/Logo.png" alt="Logo Boolflix">
      <div class="list">
                <ul>
                    <li><a href="/">Home </a></li>
                    <li><a href="#series">Serie TV</a></li>
                    <li><a href="#films">Film</a></li>
                    <li>Nuovi e Popolari</li>
                    <li>La mia lista</li>   
                </ul>
        </div> 
    <div class="account">
      <i class="fas " @click="toggle()" :class="flag ? 'fa-bell' : 'fa-bell-slash'"></i>
      <div class="user" >ANS
      </div>
      <i class="fas fa-chevron-down"></i>
    </div>
  </header>
</template>

<script>
export default {
    name:"Header",
    data:function(){
    return {
            flag: false,
        }
    },
    methods: {
        toggle: function() {
            this.flag = !this.flag;
        }
    }
}
</script>

<style lang="scss" scoped>
header{
  display:flex;
  align-items: center;
  height:80px;
  padding:10px;
  background-color:black;
  img{
    padding:0px 30px;
    height: 50%;
  }
  i{
    cursor:pointer;
  }
  .list{
    padding:0px 5px;
        ul{
            height:100%;
            width:100%;
            margin:0;
            padding:0;
            li{
                display: inline;
                padding:0px 10px;
                font-size: 14px;
                list-style: none;
                color:rgb(175, 172, 172); 
                  a{
                    color:rgb(175, 172, 172);  
                    text-decoration: none;
                      &:hover{
                      color: white;
                      }
                      }
                      &:hover{
                      color: white;    
                        }
                    }
                }
            }
  .account{
    position:absolute;
    right:0;
    display:flex;
    align-items: center;
    color:rgb(206, 204, 204);
  }
  .user{
    display:flex;
    justify-content: center;
    align-items: center;
    width:25px;
    height:25px;
    margin: 0 15px;
    padding:20px;
    color:rgb(206, 204, 204);
    background-color: rgb(218, 85, 107);
    border-radius:10%;
    font-weight: 700;
    font-size: 14px;
    cursor:pointer;
  }
  .fa-chevron-down{
    font-size:10px;
    padding-right:3px;
  }
}
</style>