<template>
    <section class="movie-card">
        <div class="card-container" @mouseenter="getCast()">
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

                    <!-- Cast  -->
                    <div class="info-line cast">
                        Cast:
                        
                        <div class="actor" v-for="(actor, index) in cast" :key="index" >
                            {{ actor.name }}
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

export default {
    name: 'MovieCard',
    props: {
        movieObject: Object,
        apiKey: String
    },
    data: function() {
        return {
            availableFlags: ['it', 'en'],
            cast: []
        }
    },
    methods: {
        getCast: function() {

            let type = '';
            if(this.movieObject.title) {
                type = 'movie';
            } else {
                type = 'tv';
            }
            console.log(type);
            console.log(this.movieObject.id);
            axios.get(
                `https://api.themoviedb.org/3/${type}/${this.movieObject.id}/credits`,
                {
                    params: {
                        api_key: this.apiKey,
                    }
                }
            ).then((response) => {
                // Avoids infinite loop 
                if(response.data.cast.length < 5) {
                    this.cast = response.data.cast;
                    console.log(this.cast);
                }else {
                    const castArray = [];

                    for( let i = 0; castArray.length < 5; i++) {
                        let thisActor = response.data.cast[i];
                        castArray.push(thisActor);
                        this.cast = castArray;
                    }
                }   
            }); 
        }
    },
    computed:{
        movieLanguage(){
            return this.movieObject.original_language
        },
        movieStar() {
           let starCount = Math.ceil(this.movieObject.vote_average / 2);
           return starCount;
        },
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
                        text-align: center;
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
                    align-items: baseline;

                    .flag {
                        width: 10%;
                        margin-left: 5px;
                    }

                    span.flag {
                        text-transform: uppercase;
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

                // Cast 
                .cast {

                    .actor {
                        margin: 10px 0;
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