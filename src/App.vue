<template>
  <div id="app">
    
    <SearchBar @updateFilter="setFilter"/>

    <Main :movies="moviesArray" :series="seriesArray"/>
    
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import Main from "./components/Main.vue";
import axios from 'axios';

export default {
  name: "App",
  components: {
    SearchBar,
    Main,
  },
  data: function() {
    return {
      apiKey: 'da14a988ea19f92a78280e6b0dc105c9',
      userSearch: '',
      moviesArray: [],
      seriesArray: []
    }
  },
  methods: {
    setFilter: function(searchText) {
      this.userSearch = searchText;
      this.getMovies();
      this.getSeries();
    },
    getMovies: function() {
      axios.get('https://api.themoviedb.org/3/search/movie', 
        {
          params: {
            api_key: this.apiKey,
            query: this.userSearch,
          }
        }
      ).then((response) => {
        this.moviesArray = response.data.results;
      });
    }, 
    getSeries: function() {
      axios.get('https://api.themoviedb.org/3/search/movie', 
        {
          params: {
            api_key: this.apiKey,
            query: this.userSearch,
          }
        }
      ).then((response) => {
        this.seriesArray = response.data.results;
      });
    }, 
  },
};
</script>

<style lang="scss">
@import './style/general.scss';


</style>
