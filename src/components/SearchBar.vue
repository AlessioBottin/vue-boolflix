<template>
    <section class="search-bar">
        <div class="container">
            <input type="text" placeholder="Inserisci il nome di un film/serie TV" v-model="userSearch">
            <button @click="$emit('updateFilter', userSearch)">Cerca</button>
        </div>
    </section>
</template>

<script>
export default {
    name: 'SearchBar',
    data: function() {
        return {
            userSearch: '',
        }
    }
}
</script>

<style lang="scss" scoped>
.search-bar {
    padding: 30px;
    .container {

        // Input 
        input {
            width: 300px;
            padding: 10px 20px;
            border-radius: 5px;
            margin: 0 10px;
            border: 1px solid lightblue;
        }

        // Button 
        button {
            padding: 10px 20px;
            border-radius: 5px;
            border: 1px solid lightblue;
        }
    }
}
</style>