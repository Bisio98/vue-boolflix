<template>
    <div class="main">
        <div class="poster">
            <div class="poster_img">
                <img class="poster_img" :src="element.poster_path ? imgFilm + element.poster_path : element.backdrop_path" alt="">
                <h2>{{ element.title ? element.title : element.name }}</h2>
            </div>
            <div class="description">
                <h3>{{ element.title ? element.title : element.name }}</h3>
                <h4>{{ element.original_title ? element.original_title : element.original_name }}</h4>
                <div class="flag"><img :src="getFlag(element.original_language)" alt=""></div>
                <div class="stars">
                    <i v-for="(star,index) in Math.ceil((element.vote_average) / 2)" :key="index" class="fas fa-star"></i>
                    <i v-for="(star,index) in ( 5 - Math.ceil((element.vote_average) / 2))" :key="index" class="far fa-star"></i>
                </div>
                <!-- <div v-if="getActors()">
                    <h4 v-for="(actor,index) in finalActors" :key="index"> {{ actor }}</h4>
                </div> -->
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "SingleCard",
    props: {
        element: Object
    },
    data: function(){
        return {
            flag: '',
            imgFilm: 'http://image.tmdb.org/t/p/w500/',
            stars: [],
            noStars: [],
            actors: [],
            finalActors: [],
            request: 'https://api.themoviedb.org/3/movie/',
            finalRequest: ''
        }
    },
    methods: {
        getFlag: function(flagInput){
            if(flagInput === 'en')
                return 'https://countryflagsapi.com/svg/' + 'usa';
            else if(flagInput === 'ja')
                return 'https://countryflagsapi.com/svg/' + 'jp';
            else{
                return 'https://countryflagsapi.com/svg/' + flagInput;
            }
        },
        getActors: function(){
            this.finalRequest = this.request + this.element.id +'/credits'
            axios.get(this.finalRequest,{
            params: {
                api_key: '69739f2b59204dc50fc56c7466acc9d8',
                language: 'en-US'
            }
            }).then((response) => {
                this.actors = response.data;
                }
            )
            for(let i= 0; i < 5; i++){
                this.finalActors.push( this.actors.cast[i]);
            }
        }
    },
        
}
</script>

<style lang="scss" scoped>
    .main{
        display: flex;
        flex-direction: column;

        .poster{
        width: 250px;
        height: 350px;
        border: 1px solid red;
        position: relative;

            &:hover {
                cursor: pointer;
            }

            &:hover .description{
                display: flex;
            }

            .poster_img{
                position: relative;
                width: 248px;
                height: 348px;
                z-index: 1;
            }

            h2{
                position: absolute;
                top: 50%;
                left: 50%;
                z-index: 0;
                transform: translate(-50%,-50%);
            }

            .description{
                position: absolute;
                top: 0;
                left: 0;
                width: 248px;
                height: 348px;
                align-items: center;
                justify-content: space-evenly;
                flex-direction: column;
                display: none;
                z-index: 2;
                text-align: center;

                .flag{
                    width: 30px;
                    height: 10px;
                }

                h3{
                    font-size: 20px;
                }

                h4{
                    font-size: 18px;
                }

            }
        }
    }
    
</style>