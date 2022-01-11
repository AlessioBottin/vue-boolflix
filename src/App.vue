<template>
  <div id="app">
    
    <SearchBar @updateFilter="setFilter"/>

    <main>
      <MovieCard v-for="(movie, index) in moviesArray" :key="index" :movieObject="movie"/>
    </main>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import MovieCard from "./components/MovieCard.vue";
import axios from 'axios';

export default {
  name: "App",
  components: {
    SearchBar,
    MovieCard,
  },
  data: function() {
    return {
      userSearch: '',
      moviesArray: [],
    }
  },
  methods: {
    getMovies: function() {
      axios.get('https://api.themoviedb.org/3/search/movie', 
        {
          params: {
            api_key: 'da14a988ea19f92a78280e6b0dc105c9',
            query: this.userSearch,
          }
        }
      ).then((response) => {
        this.moviesArray = response.data.results;
      });
    }, 
    setFilter: function(searchText) {
      this.userSearch = searchText;
      this.getMovies();
    }
  },
};
</script>

<style lang="scss">
@import './style/general.scss';

main {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>
