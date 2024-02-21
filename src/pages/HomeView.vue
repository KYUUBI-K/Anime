<template>
  <div class="popular">
    <!-- <div class="about_anime"></div> -->
    <div class="text_anim">
      <h5>Best Animes</h5>
    </div>
    <div
      class="top_animes"
      v-for="anime in animeStore.animes"
      :key="anime.mal_id"
    >
      <div @click="ToCard(anime.mal_id)" class="anime_item">
        <img class="anime_img" :src="anime.images.jpg.image_url" alt="err" />
      </div>
      <div class="anime_item anime_title">{{ anime.title_english }}</div>
    </div>
  </div>
  <router-link class="to_anime" to="/animes">Animes</router-link>
</template>
<script>
import { useAnimeStore } from "@/stores/animes";
import { onMounted } from "vue";
import router from "@/router";
export default {
  setup() {
    const animeStore = useAnimeStore();
    onMounted(() => {
      // animeStore.getAnimes();
      animeStore.getPopularAnimes();
    });
    const ToCard = (itemId) => {
      router.push({
        name: "anime",
        params: { id: itemId },
      });
      console.log(itemId);
    };
    return { animeStore, ToCard };
  },
};
</script>
<style>
.about_anime {
  display: flex;
  margin-bottom: 2rem;
  color: #c8c8c8;
  line-height: 1.6;
  padding-bottom: 1rem;
  border-bottom: 1px solid #0f3beb;
}
.text_anim {
  color: #7c7a7a;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
}
.to_anime {
  color: #0f3beb;
  border-bottom: 1px dotted #0f30b5;
  text-decoration: none;
  display: flex;
  justify-content: center;
}
.to_anime:hover {
  color: #051b74;
  border-bottom: 1px dotted #051b74;
}
.top_animes {
  display: inline-block;
  /* width: 150px; */
  max-height: 100%;
  margin-bottom: 20px;
  margin-left: 85px;
}
.anime_item {
  text-decoration: none;
}
.anime_title {
  display: flex;
  max-width: 150px;
}
.anime_img {
  width: 200px;
  height: 250px;
}
.anime_img:hover {
  padding: 10px;
}
</style>
