<script setup lang="ts">
interface Anime {
  author: string;
  date: string;
  postid: string;
}
const title = ref(useRoute().params.title);
const fetchAnimes = async () =>
  $fetch<Anime[]>("https://l6yobvv4dg.execute-api.ap-northeast-1.amazonaws.com/demo/comment", {
    params: {
      author: title.value,
      postid:"",
    },
  });
const { data: animes } = useAsyncData("animes", () => fetchAnimes());
const search = async () => (animes.value = await fetchAnimes());
</script>

<template>
  <main class="container">
    <h1>search anime</h1>
    <div class="grid">
      <input v-model="title" />
      <button @click="search">search</button>
    </div>
    <table>
      <tr v-for="anime in animes">
        <td>{{ anime.author }}</td>
        <td>{{ anime.date }}</td>
        <td>{{ anime.postid }}</td>
      </tr>
    </table>
  </main>
</template>
