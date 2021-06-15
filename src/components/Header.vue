<template>
  <header>
    <img src="../assets/Logo.png" alt="Logo Boolflix">
    <div class="account">
      <i class="fas " @click="toggle()" :class="flag ? 'fa-bell' : 'fa-bell-slash'"></i>
      <div class="user" >ANS
      </div>
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
  justify-content: space-between;
  align-items: center;
  height:80px;
  padding:10px;
  background-color:black;
  img{
    padding-left:15px;
    height: 100%;
  }
  i{
    cursor:pointer;
  }
  .account{
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
    border-radius:50%;
    font-weight: 700;
    font-size: 14px;
    cursor:pointer;
  }
  
}
</style>