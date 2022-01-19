<template>
  <div id="app">
    <Header @search="searchMovies" />
    <Body :films="foundFilms" :series="foundTv" />
  </div>
</template>

<script>
import Body from "./components/Body.vue";
import Header from "./components/Header.vue";
import axios from 'axios';

export default {
  name: "App",
  components: {
    Body,
    Header
  },
  data: function(){
    return {
      searched: '',
      foundFilms: [],
      foundTv: [],
    }
  },
  methods: {
    searchMovies: function(elementSearched){
      this.searched = elementSearched;
      this.searchFilmsInApi();
      this.searchSeriesInApi();
      this.searchActorsInApi();
    },
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
    )}
  }
};
</script>

<style lang="scss">
  @import './style/general.scss';
  div{
    background-color: #141414;
    color: white;
  }
</style>
