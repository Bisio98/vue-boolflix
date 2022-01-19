<template>
    <section class="container">
        <div class="list">
            <h2>FILMS</h2>
            <div class="film_container">
                <SingleCard class="card" v-for="(singleMovie,index) in films" :key="index" :element="singleMovie" />
            </div>

            <h2>TV SERIES</h2>
            <div class="film_container">
                <SingleCard class="card" v-for="(singleSerie,index) in series" :key="index" :element="singleSerie" />
            </div>
        </div>
    </section>
</template>

<script>
import SingleCard from './SingleCard.vue';

export default {
  components: { 
        SingleCard 
    },
    name: "Body",
    props: {
        films: Array,
        series: Array
    },
    
}
</script>

<style lang="scss" scoped>
@import '../style/common.scss';
    section{
        height: calc(100vh - 100px);
        overflow-y: auto;

        .film_container{
            display: flex;
            overflow-x: auto;

            .card{
            margin: 5px 20px;
            }
        }
    }  
</style>