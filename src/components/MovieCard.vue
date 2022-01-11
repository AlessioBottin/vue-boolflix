<template>
    <section class="movie-card">
        <div class="container">
            <ul>
                <li>{{ movieObject.title }}</li>
                <li>{{ movieObject.original_title }}</li>
                <li>{{ movieObject.original_language }}</li>
                <li>{{ movieObject.vote_average }}</li>
            </ul>
        </div>
    </section>
</template>
<script>
export default {
    name: 'MovieCard',
    props: {
        movieObject: Object
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