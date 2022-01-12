<template>
    <section class="serie-card">
        <div class="container">
            <ul>
                <div v-if="serieObject.poster_path !== null" class="poster">
                    <img :src="'https://image.tmdb.org/t/p/w342' + serieObject.poster_path" :alt="serieObject.name">
                </div>
                <li>Titolo: {{ serieObject.name }}</li>
                <li>Titolo originale: {{ serieObject.original_name }}</li>
                <li>
                    Lingua originale: 
                    
                    <img v-if="availableFlags.includes(serieLanguage)" 
                        :src="require('../assets/img/'+serieLanguage+'.png')" 
                        :alt="serieLanguage+'flag'"
                    >

                    <span v-else class="flag">{{serieLanguage}}</span>
                </li>
                <li>Voto: {{ serieObject.vote_average }}</li>
            </ul>
        </div>
    </section>
</template>
<script>
export default {
    name: 'MovieCard',
    props: {
        serieObject: Object,
    },
    data: function() {
        return {
            availableFlags: ['it', 'en'],
        }
    },
    computed:{
        serieLanguage(){
            return this.serieObject.original_language
        }
    }
}
</script>

<style lang="scss" scoped>
.serie-card {
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