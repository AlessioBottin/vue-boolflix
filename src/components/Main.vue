<template>
    <main>
        <div class="container">

            <!-- Films  -->
            <h2>Film</h2>
            <div class="movie-container">
                <MovieCard v-for="(movie, index) in movies" :key="index" :movieObject="movie"/>
            </div>

            <!-- TV Series  -->
            <h2>TV Series</h2>
            <div class="movie-container">
                <MovieCard v-for="(serie, index) in series" :key="index" :serieObject="serie"/>
            </div>

        </div>
    </main>
</template>

<script>
import MovieCard from "./MovieCard.vue";

export default {
    name: 'Main',
    components: {
        MovieCard
    },
    props: {
        movies: Array,
        series: Array
    },
}
</script>

<style lang="scss" scoped>
main {

  .movie-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
      
  }
}
</style>