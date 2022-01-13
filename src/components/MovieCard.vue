<template>
    <section class="movie-card">
        <div class="container">
            <ul>
                <!-- Poster  -->
                <div v-if="movieObject.poster_path !== null" class="poster">
                    <img :src="'https://image.tmdb.org/t/p/w342' + movieObject.poster_path" :alt="movieObject.name">
                </div>

                <!-- Title  -->
                   <!-- if movieObject.title exist then                else  -->
                <li>Titolo: {{ movieObject.title ? movieObject.title : movieObject.name }}</li>
                <li>Titolo originale: {{ movieObject.original_title ? movieObject.original_title : movieObject.original_nam }}</li>

                <!-- Language  -->
                <li>
                    Lingua originale: 

                    <!-- Flag image if available   -->
                    <img v-if="availableFlags.includes(movieLanguage)" 
                        :src="require('../assets/img/'+movieLanguage+'.png')" 
                        :alt="movieLanguage+'flag'"
                    >

                    <!-- Language text  -->
                    <span v-else class="flag">{{movieLanguage}}</span>
                </li>

                <!-- Rating  -->
                <li>Voto: 
                    <span class="vote">
                        <div class="yellow" v-for="star in movieStar" :key="star"><i class="fas fa-star"></i></div>
                        <div class="grey" v-for="greyStar in (5 - movieStar)" :key="greyStar+'grey'"><i class="fas fa-star"></i></div>
                    </span>
                </li>
            </ul>
        </div>
    </section>
</template>
<script>
export default {
    name: 'MovieCard',
    props: {
        movieObject: Object,
    },
    data: function() {
        return {
            availableFlags: ['it', 'en'],
        }
    },
    computed:{
        movieLanguage(){
            return this.movieObject.original_language
        },
        movieStar() {
           let starCount = Math.ceil(this.movieObject.vote_average / 2);
           return starCount;
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/utilities.scss';
@import '../style/variables.scss';


.movie-card {
    border: 1px solid black;
    width: calc( (100% / 10) - 10px);
    text-align: center;
    margin: 0 5px 10px 5px;
    flex-shrink: 0;

    .container {
        
        ul {

            li {
               margin-bottom: 5px; 

                .vote {
                   display: flex;
                   flex-wrap: wrap;
                   justify-content: center;

                    .yellow {
                       color: yellow;
                       display: flex;
                       flex-wrap: wrap
                    }

                    .gray {
                       color: gray;
                       display: flex;
                       flex-wrap: wrap
                    }
                }
            }
            
        }
    }
}
</style>