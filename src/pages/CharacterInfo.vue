<template>
  <div class="character-box">
    <div>
      <img
        class="character-img"
        :src="animeStore.character.images?.jpg?.image_url"
        alt=""
      />
      <div class="character-info-box">
        <div class="character-name">
          Name: {{ animeStore.character.name }}({{
            animeStore.character.name_kanji
          }})
        </div>
      </div>
    </div>
    <div class="character">
      <div class="description">Description:</div>
      <div class="character-about">{{ animeStore.character.about }}</div>
    </div>
  </div>
</template>

<script>
import { useAnimeStore } from "@/stores/animes";
import { onMounted } from "vue";
import router from "@/router";
export default {
  setup() {
    const animeStore = useAnimeStore();
    onMounted(async () => {
      await animeStore.getCharacter(router.currentRoute.value.params.id);
    });
    return { animeStore };
  },
};
</script>

<style lang="css" scoped>
.character-box {
  display: flex;
}

.character-info-box {
  color: #e6d9d9;

  line-height: 2rem;
}
.character-img {
  width: 312px;
  height: 450px;
}
.character-name {
  font-size: 1.4rem;
  margin: 1rem 0;
}
.character {
  margin-left: 50px;
  margin-top: 30px;
  margin-bottom: 20px;
}
.character-about {
  font-size: 1.6rem;
  /* margin-bottom: 5rem; */
  color: #e6d9d9;
}
</style>
