<template>
  <div id="app">
    
    <Header @setUserSearch="setFilter"/>

    <Main :movies="moviesArray" :series="seriesArray"/>
    
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Header from "./components/Header.vue";
import axios from 'axios';

export default {
  name: "App",
  components: {
    Header,
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
    setFilter: function(userSearchText) {
      this.userSearch = userSearchText;
      this.getMovies();
      this.getSeries();
    },
    getMovies: function() {
      axios.get(
        'https://api.themoviedb.org/3/search/movie', 
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
      axios.get(
        'https://api.themoviedb.org/3/search/tv', 
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
@import './style/utilities.scss';

// Scrollbar 
html::-webkit-scrollbar {
  width: 0.8vw;
}

html::-webkit-scrollbar-thumb {
  background-color: $brand_color; 
  border-radius: 7px;

  &:hover {
    background-color: rgb(255, 57, 57)
  }
}

html::-webkit-scrollbar-track {
  background-color: rgb(65, 65, 65);
}

// Firefox 
html {
  scrollbar-color: $brand_color rgb(65, 65, 65);
  scrollbar-width: 0.8vw;
}

// Slider 
// html::-webkit-slider-thumb {
//   background-color: $brand_color; 
//   border-radius: 7px;

//   &:hover {
//     background-color: rgb(255, 57, 57)
//   }
// }

// html::-webkit-slider-runnable-track {
//   background-color: rgb(65, 65, 65);
// }

// html::-webkit-slider {
//   height: 10px;
// }

// Scrollbar horizontal
html::-webkit-scrollbar:horizontal {
  height: 20px;
}

html::-webkit-scrollbar-thumb:horizontal {
  background-color: $brand_color; 
  border-radius: 7px;

  &:hover {
    background-color: rgb(255, 57, 57)
  }
}

html::-webkit-scrollbar-track:horizontal {
  background-color: rgb(65, 65, 65);
}

</style>
