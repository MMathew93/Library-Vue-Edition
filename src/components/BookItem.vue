<template>
    <div class="book-item">
        <div class="cover">
            <h2> "{{book.title}}" </h2>
        </div>
        <h4> Author: {{book.author}} </h4>
        <br>
        <h4> {{book.pages}} pages </h4>
        <br>
        <h4 v-if="book.read"> I have read and enjoyed this book! </h4>
        <h4 v-else> This is on my list to read! </h4>
        <button @click="$emit('del-book', book.id)" class="del">Remove</button>
    </div>
</template>

<script>
export default {
    name: "bookitem",
    props:["book"]
}
</script>

<style scoped>
    .book-item {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        color: white;
        border: 2px solid white;
        margin: 25px;
        padding: 5%;
        text-align: center;
        width:500px;
        min-height: 300px;
    }

    .cover {
        background-color: #1a1a1a;
        text-decoration: underline;
        border: 5px solid white;
        padding: 10px;
    }

    .del {
        border-radius: 50px;
        font-size: 20px;
        width:33%;
        border: white;
    }

    .del:hover {
        background-color: rgb(156, 12, 12);
        color: white;
    }
</style>