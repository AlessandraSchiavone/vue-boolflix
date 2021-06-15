<template>
  <aside :class="status ? 'active' : ''" >
        <input type="text" placeholder="Cerca "
            v-if="status"
            @keydown.enter="$emit('performSearch', searchText)"
            @keyup.enter="toggleSearch"
            v-model="searchText">
            <div class="icon-cont">
            <div class="btn-cont" >
                <i class="fas fa-search" @click="toggleSearch" :class="status ? 'active' : ''"></i>
                <span v-if="status">Cerca</span>
            </div>
            <div class="list btn-cont">
                <ul v-if="status">
                    <li><a href="/">Home Page</a></li>
                    <li><a href="#films">Film</a></li>
                    <li><a href="#series">Serie TV</a></li>
                    <li>Drammi</li>
                    <li>Horror</li>
                    <li>Originali Netflix</li>
                    <li>Documentari</li>
                    <li>Film per bambini</li>
                    <li>Commedie</li>
                    <li>Film premiati</li>
                    <li>Film italiani</li>
                    <li>Film internazionali</li>
                    <li>Disponibili per il download</li>     
                </ul>
            </div> 
        </div>
    </aside>
</template>

<script>
export default {
    name:"Aside",
    data: function() {
        return {
            status: false,
            searchText: '',
        }
    },
    methods: {
    toggleSearch: function() {
            this.status = !this.status
            this.searchText = ""
        }
    }
}
</script>

<style lang="scss" scoped>
aside {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 70px;
        height: calc(100vh -  80px);
        background-color:  black;
        &.active {
            width:300px;
        }
        input {
            padding: 10px;
            border-radius: 12px;
            border: 3px solid grey;
            background-color: transparent;
            color: white;
            outline: none;  
            &:focus {
                border: 2px solid white;
            }
        }
        .icon-cont {
            display: flex;
            flex-direction: column;
            width:100%;
            margin: 30px 0;
            color:rgb(175, 172, 172);  
            cursor:pointer;
            .btn-cont {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                text-align: center;
                width:100%;
                padding:20px 2px;
                cursor: pointer;
                &:hover i{
                    color: white;
                }
            }
            .list{
                ul{
                   height:100%;
                    width:100%;
                    margin:0;
                    padding:0;
                    
                    li{
                        text-align: left;
                        padding:10px 0px;
                        font-size: 18px;
                        list-style: none;
                        a{
                            color:rgb(175, 172, 172);  
                            text-decoration: none;
                            &:hover{
                            color: white;
                            }
                        }
                        &:hover{
                            color: white;
                            background-color:grey ;
                        }
                    }
                }
            }   
        }
    }
</style>