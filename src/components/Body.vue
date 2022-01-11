<template>
    <div>
        <input v-model="searched" type="text">
        <button @click="searchInApi">Cerca</button>
        <ul>
            <li v-for="(element,index) in found" :key="index">
                <div>{{ element.title }}</div>
                <div>{{ element.original_title }}</div>
                <div>{{ element.original_language }}</div>
                <div>{{ element.vote_average }}</div>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Body",
    data: function(){
        return {
            searched: '',
            found: []
        }
    },
    methods: {
        searchInApi: function(){
            axios.get('https://api.themoviedb.org/3/search/movie',{
                params: {
                    api_key: '69739f2b59204dc50fc56c7466acc9d8',
                    query: this.searched
                }
            }).then((response) => {
                this.found = response.data.results;
                console.log(this.found);
            }
        )}
    }
}
</script>

<style lang="scss" scoped>

</style>