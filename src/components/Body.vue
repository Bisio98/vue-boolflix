<template>
    <div>
        <input v-model="searched" type="text">
        <button @click="searchFilmsInApi(); searchSeriesInApi();">Cerca</button>
        <div class="list">
            <h2>FILMS</h2>
            <ul>
                <li v-for="(element,index) in foundFilms" :key="index">
                    <div><img :src="imgFilm + element.poster_path" alt=""></div>
                    <div>{{ element.title }}</div>
                    <div>{{ element.original_title }}</div>
                    <div><img :src="getFlag(element.original_language)" alt=""></div>
                    <div>{{ Math.ceil((element.vote_average) / 2) }}</div>
                    <div>
                        <i v-for="(star,index) in Math.ceil((element.vote_average) / 2)" :key="index" class="fas fa-star"></i>
                        <i v-for="(star,index) in ( 5 - Math.ceil((element.vote_average) / 2))" :key="index" class="far fa-star"></i>
                    </div>
                </li>
            </ul>
        
            <h2>TV SERIES</h2>
            <ul>
                <li v-for="(element,index) in foundTv" :key="index">
                    <div><img :src="imgFilm + element.backdrop_path" alt=""></div>
                    <div>{{ element.name }}</div>
                    <div>{{ element.original_name }}</div>
                     <div>
                        <i v-for="(star,index) in Math.ceil((element.vote_average) / 2)" :key="index" class="fas fa-star"></i>
                        <i v-for="(star,index) in ( 5 - Math.ceil((element.vote_average) / 2))" :key="index" class="far fa-star"></i>
                    </div>
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
            flag: '',
            imgFilm: 'http://image.tmdb.org/t/p/w500/',
            stars: [],
            noStars: []
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
    },
    
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