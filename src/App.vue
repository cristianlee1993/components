<script setup>
// import ButtonCounter from './components/ButtonCounter.vue'
import BlogPost from './components/BlogPost.vue'
import { computed, onMounted, ref } from 'vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);

const postXpage = 5;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
};
const prev = () => {
  inicio.value += - postXpage;
  fin.value += - postXpage;
}

const favorito = ref('')
const cambiarFavorito = (title) => {
  favorito.value = title;
};

onMounted(async () => {
  loading.value = true;
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json();

  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false
  }
  // fetch('https://jsonplaceholder.typicode.com/posts')
  //   .then((res) => res.json())
  //   .then((data) => { posts.value = data; })
  //   .finally(() => loading.value = false);
});



const maxLength = computed(() => posts.value.length);
</script>



<template>
  <div class="container">
    <LoadingSpinner v-if="loading"></LoadingSpinner>
    <h1>APP</h1>
    <h2>Mis post Favoritos: {{ favorito }}</h2>

    <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxLength="maxLength" class="mb-2">
    </PaginatePost>

    <BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id" :body="post.body"
      @cambiarFavoritoNombre="cambiarFavorito" class="mb-2">
    </BlogPost>

  </div>
</template>