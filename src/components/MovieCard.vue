<template>
    <section class="movie-card">
        <div class="container">
            <ul>
                <li>Titolo: {{ movieObject.title }}</li>
                <li>Titolo originale: {{ movieObject.original_title }}</li>
                <li v-html="getLanguageFlag()"></li>
                <li>Voto: {{ movieObject.vote_average }}</li>
            </ul>
        </div>
    </section>
</template>
<script>
export default {
    name: 'MovieCard',
    props: {
        movieObject: Object,
        serieObject: Object
    },
    data: function() {
        return {
            availableFlags: ['it', 'en'],
            movieLanguage: this.movieObject.original_language,
            flagPath: '',
        }
    },
    methods: {
        getLanguageFlag: function() {

            if( this.availableFlags.includes(this.movieLanguage) ) {
                this.flagPath = `Lingua originale: <img src="require(../assets/img/${this.movieLanguage}.png)" alt="${this.movieLanguage} flag">`;
            }else {
                this.flagPath = `Lingua originale: <span class="flag">${this.movieLanguage}<span/>`;
            }

            return this.flagPath;
        }
    }
}
</script>

<style lang="scss" scoped>
.movie-card {
    border: 1px solid black;
    width: calc( (100% / 10) - 10px);
    text-align: center;
    margin-bottom: 10px;

    .container {
        
        ul {

            li {
               margin-bottom: 5px; 
            }
        }
    }
}
</style>