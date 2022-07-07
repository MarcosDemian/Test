<template>
    <div id="search-container">
        <input type="text" v-model="query" v-on:input="$emit('query-change', query)"
        placeholder="🔎 Buscar">
    </div>
</template>

<script>
export default {
    name: 'Search',
    data(){
        return {
            query: ''
        }
    }
}
</script>

<style scoped>
    #search-container{
        width: 600px;
        margin: 0 auto;
        padding: 0 10px 0 10px;
    }

    input{
        border-radius: 20px;
        padding: 10px;
        width: 100%;
        outline: none;
        border: solid 1px #ccc;
    }
    
    input::placeholder{
        color: #1d2730;
        font-family: Gulzar, sans-serif;
    }
</style>