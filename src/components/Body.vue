<template>
    <div>
        <input v-model="searched" type="text">
        <button @click="searchFilmsInApi(); searchSeriesInApi();">Cerca</button>
        <div class="list">
            <h2>FILMS</h2>
            <ul>
                <li v-for="(element,index) in foundFilms" :key="index">
                    <div>{{ element.title }}</div>
                    <div>{{ element.original_title }}</div>
                    <div><img :src="getFlag(element.original_language)" alt=""></div>
                    <div>{{ element.vote_average }}</div>
                </li>
            </ul>
        
            <h2>TV SERIES</h2>
            <ul>
                <li v-for="(element,index) in foundTv" :key="index">
                    <div>{{ element.name }}</div>
                    <div>{{ element.original_name }}</div>
                    <div>
                        <img v-if="getFlag(element.original_language)" :src="getFlag(element.original_language)" alt="">
                        <span v-else>{{ element.original_language }}</span>
                    </div>
                    <div>{{ element.vote_average }}</div>
                </li>
            </ul>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Body",
    data: function(){
        return {
            searched: '',
            foundFilms: [],
            foundTv: [],
            flag: ''
        }
    },
    methods: {

        searchFilmsInApi: function(){
            axios.get('https://api.themoviedb.org/3/search/movie',{
                params: {
                    api_key: '69739f2b59204dc50fc56c7466acc9d8',
                    query: this.searched
                }
            }).then((response) => {
                this.foundFilms = response.data.results;
                console.log(this.foundFilms);
            }
        )},
        searchSeriesInApi: function(){
            axios.get('https://api.themoviedb.org/3/search/tv',{
                params: {
                    api_key: '69739f2b59204dc50fc56c7466acc9d8',
                    query: this.searched
                }
            }).then((response) => {
                this.foundTv = response.data.results;
                console.log(this.foundTv);
            }
        )},
        getFlag: function(flagInput){
            if(flagInput === 'en')
                return 'https://countryflagsapi.com/svg/' + 'usa';
            else if(flagInput === 'ja')
                return 'https://countryflagsapi.com/svg/' + 'jp';
            else{
                return 'https://countryflagsapi.com/svg/' + flagInput;
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    img{
        width: 100px;
    }

    .list{
        display: flex;
    }

    ul{
        list-style: none;
        
        li{
            display: flex;
            flex-direction: row;

            div{
                margin: 10px;
            }
        }
    }
</style>