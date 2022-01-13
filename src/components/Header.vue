<template>
    <header>
        <div class="container">
            <!-- Logo  -->
            <h1 class="title">Boolflix</h1>

            <!-- SearchBar  -->
            <div class="search-bar">
                <SearchBar @updateSearch="emitFilter"/>
            </div>
        </div>
    </header>
</template>

<script>
import SearchBar from './SearchBar.vue'
export default {
    name: 'Header',
    components: {
        SearchBar,
    },
    methods: {
        emitFilter: function(userSearch) {
            this.$emit('setUserSearch', userSearch);
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/variables.scss';
header { 
    background-color: black;
    padding: 20px 0;

    .container {
        display: flex;
        justify-content: space-between;

        // Title 
        .title {
            color: $brand_color;
            text-transform: uppercase;
            font-size: 30px;
        }

        // SearchBar 
        // .search-bar {

        // }
    }

}
</style>