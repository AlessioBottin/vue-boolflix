<template>
    <main>
        <div class="container">

            <!-- Films  -->
            <h2>Film</h2>
            <div class="movie-container">
                <MovieCard v-for="(movie, index) in movies" :key="index" :movieObject="movie"/>
            </div>

            <!-- TV Series  -->
            <h2 class="tv">TV Series</h2>
            <div class="movie-container">
                <MovieCard v-for="(serie, index) in series" :key="index" :movieObject="serie"/>
            </div>

        </div>
    </main>
</template>

<script>
import MovieCard from "./MovieCard.vue";

export default {
    name: 'Main',
    components: {
        MovieCard,
    },
    props: {
        movies: Array,
        series: Array
    },
}
</script>

<style lang="scss" scoped>
@import '../style/utilities.scss';
@import '../style/variables.scss';

// Scrollbar 
.movie-container::-webkit-scrollbar {
  width: 0.4vw;
  height: 10px;
}

.movie-container::-webkit-scrollbar-thumb {
  background-color: $brand_color; 
  border-radius: 7px;
}

.movie-container::-webkit-scrollbar-track {
  background-color: #181818;
}

// Firefox 
.movie-container {
  scrollbar-color: $brand_color #181818;
  scrollbar-width: 0.4vw;
}

main {
   background-color: #181818; 
   color: white;
   padding: 60px 0;

    .container {

        h2 {
            font-size: 50px;
            margin: 30px 0;
        }

       .movie-container {
            display: flex;
            justify-content: left;
            overflow-x: auto;
            padding-bottom: 50px;

            .movie-card:first-child {
                margin-left: 0;
            }
        }
    }

  
}
</style>