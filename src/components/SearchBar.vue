<template>
    <section class="search-bar">
        <div class="container">
            <input type="text" @keyup.enter="$emit('updateSearch', userSearch)" placeholder="Inserisci il nome di un film/serie TV" v-model="userSearch">
            <button @click="$emit('updateSearch', userSearch)" class="btn">Cerca</button>
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
@import '../style/utilities.scss';

.search-bar {
    .container {
        display: flex;

        // Input 
        input {
            width: 300px;
            padding: 10px 20px;
            margin: 0 10px;
            outline: none;
            border-radius: 10px;
            color: white;
            border: 2px solid white;
            background-color: black;
            display: inline-block;
        }
        

        // Button 
    }
}
</style>