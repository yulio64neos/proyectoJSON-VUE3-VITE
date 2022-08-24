<script setup>
import BlogPost from "./components/BlogPost.vue";
import { ref } from 'vue';

const posts = ref([]);

const favorito = ref("");
const cambiarFavorito = (title) => {
  favorito.value = title;
}

fetch('https://jsonplaceholder.typicode.com/posts')
  .then((res) => res.json())
  .then((data) => {
    posts.value = data;
    console.log(data)
  })
</script>
<template>
  <div class="container">
    <h1>APP - API</h1>
    <h2>Mis post Favoritos: {{favorito}}</h2>
    <BlogPost
      v-for="(po, index) in posts"
      :key="index"
      :title="po.title"
      :id="po.id"
      :body="po.body"
      :cambiarFavorito = "cambiarFavorito"
    >
    </BlogPost>
  </div>
</template>
