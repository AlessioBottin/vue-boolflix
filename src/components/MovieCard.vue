<template>
    <section class="movie-card">
        <div class="card-container">
            <ul>
                <!-- Poster  -->
                <li class="poster">

                    <!-- if there is a poster  -->
                    <img v-if="movieObject.poster_path !== null" 
                        :src="'https://image.tmdb.org/t/p/w342' + movieObject.poster_path" 
                        :alt="movieObject.name"
                    >

                    <!-- Alternative poster  -->
                    <div v-else class="alternative-image">
                        <div class="logo">boolflix</div>
                        <div class="title">{{movieObject.title ? movieObject.title : movieObject.name}}</div>
                    </div>
                </li>

                <!-- Movie Info  -->
                <li class="movie-info">
                    <!-- Title  -->
                    <!-- if movieObject.title exist then                else  -->
                    <div class="info-line">Titolo: {{ movieObject.title ? movieObject.title : movieObject.name }}</div>
                    <div class="info-line">Titolo originale: {{ movieObject.original_title ? movieObject.original_title : movieObject.original_nam }}</div>

                    <!-- Language  -->
                    <div class="info-line language">
                        Lingua originale: 

                        <!-- Flag image if available   -->
                        <img v-if="availableFlags.includes(movieLanguage)" 
                            :src="require('../assets/img/'+movieLanguage+'.png')" 
                            :alt="movieLanguage+'flag'"
                            class="flag"
                        >

                        <!-- Language text  -->
                        <span v-else class="flag">{{movieLanguage}}</span>
                    </div>

                    <!-- Rating  -->
                    <div class="info-line rating">Voto: 
                        <span class="vote">
                            <div class="yellow" v-for="star in movieStar" :key="star"><i class="fas fa-star"></i></div>
                            <div class="grey" v-for="greyStar in (5 - movieStar)" :key="greyStar+'grey'"><i class="fas fa-star"></i></div>
                        </span>
                    </div>
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
    width: calc( (100% / 7) - 10px);
    margin: 0 5px 10px 5px;
    flex-shrink: 0;

    .card-container {
        height: 100%;

        ul {
            height: 100%;
            background-color: black;
            
            // Card Content 
            li { 
               height: 100%;

                // Poster 
                &.poster {
                    display: flex;
                    flex-direction: column;
                    justify-content: center;
                }

                // Alternative image
                .alternative-image {
                    text-transform: uppercase;
                    color: $brand_color;
                    background-color: black;
                    font-weight: bold;
                    height: 100%;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    flex-direction: column;

                    .logo {
                        font-size: 1.6vw;
                    }

                    .title {
                        font-size: 1.3vw;
                    }
                }

                // Movie Info 
                &.movie-info {
                   padding: 15px;
                   font-size: 0.8vw; 
                }

                // Info lines 
                .info-line {
                    margin-bottom: 10px;
                    font-weight: bold;
                }

                // Language 
                .language {
                    display: flex;
                    flex-direction: row;
                    align-items: flex-end;

                    .flag {
                        width: 10%;
                        margin-left: 5px;
                    }
                }

                // Rating 
                .rating {
                    display: flex;
                    flex-direction: row;
                    align-items: normal;
                }

                .vote {
                   display: flex;
                   flex-wrap: wrap;
                   justify-content: center;
                   margin-left: 5px;

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

            // Hover effect 
            .movie-info {
                display: none;
            }

            &:hover .poster {
                display: none;
            }

            &:hover .movie-info {
                display: block;
            }
            
        }
    }
}
</style>