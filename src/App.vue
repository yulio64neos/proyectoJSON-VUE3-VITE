<script setup>
import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import { ref, computed, onMounted } from "vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorito = ref("");
const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
};

const previus = () => {
  // fin.value = fin.value - postXpage
  // inicio.value = inicio.value - postXpage
  inicio.value += -postXpage;
  fin.value += -postXpage;
};

// onMounted(() => {
//   loading.value = true;
//   fetch('https://jsonplaceholder.typicode.com/posts')
//     .then((res) => res.json())
//     .then((data) => {
//       posts.value = data;
//       console.log(data)
//     })
//     .finally(() => {
//       setTimeout(() => {
//         loading.value = false
//       }, 2000)
//     })
// })
// onMounted(async() => {
//   //loading.value = true;
//   try{
//     const res = await fetch("https://jsonplaceholder.typicode.com/posts")
//     posts.value = await res.json()
//   }
//   catch(error){
//     console.log(error)
//   }
//   finally{
//     setTimeout(() => {
//       loading.value = false
//     }, 2000)
//   }
// })

const fetchData = async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }
};

fetchData()

const maxLength = computed(() => {
  posts.value.length;
});
</script>
<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>APP - API</h1>
    <h2>Mis post Favoritos: {{ favorito }}</h2>

    <!-- <button @click="next">Next provisorio</button>
    <button @click="previus">Previus provisorio</button> -->

    <PaginatePost
      class="mt-2"
      :next="next"
      :previus="previus"
      :inicio="inicio"
      :maxLength="posts.length"
      :fin="fin"
    />
    <BlogPost
      v-for="(po, index) in posts.slice(inicio, fin)"
      :key="index"
      :title="po.title"
      :id="po.id"
      :body="po.body"
      :cambiarFavorito="cambiarFavorito"
      class="mb-2"
    >
    </BlogPost>
  </div>
</template>
