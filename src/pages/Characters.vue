<template>
  <div>
    <div>
      <form class="header_search" @submit.prevent="GetSearched()">
        <input
          class="input"
          type="search"
          placeholder="Search..."
          required
          v-model="search_q"
        />
      </form>
    </div>
    <div
      class="top_animes"
      v-for="character in animeStore.characters"
      :key="character.mal_id"
    >
      <div @click="ToCard(character.mal_id)" class="anime_item">
        <img
          class="anime_img"
          :src="character.images.jpg.image_url"
          alt="err"
        />
        <div class="anime_title">{{ character.name }}</div>
      </div>
    </div>
    <div
      v-if="(page === 1) & animeStore.pagin.has_next_page"
      class="pagination"
    >
      <div class="page">{{ page }}</div>
      <button @click="NextPage()" class="next_page">
        <span>next page</span>
      </button>
    </div>
    <div v-else-if="(page === 1) & !animeStore.pagin.has_next_page"></div>
    <div class="pagination" v-else-if="!animeStore.pagin.has_next_page">
      <button @click="PreviousPage()" class="previous_page">
        <span>previous page</span>
      </button>
      <div class="page">{{ page }}</div>
    </div>
    <div class="pagination" v-else>
      <button @click="PreviousPage()" class="previous_page">
        <span>previous page</span>
      </button>
      <div class="page">{{ page }}</div>
      <button @click="NextPage()" class="next_page">
        <span>next page</span>
      </button>
    </div>
  </div>
</template>

<script>
import { useAnimeStore } from "@/stores/animes";
import { onMounted, ref } from "vue";
import router from "@/router";

export default {
  setup() {
    const page = ref(1);
    const animeStore = useAnimeStore();
    const search_q = ref("");
    const NextPage = () => {
      page.value += 1;
      animeStore.getSearchedCharacter(page.value);
    };
    const PreviousPage = () => {
      page.value -= 1;
      animeStore.getSearchedCharacter(page.value);
    };
    const GetSearched = () => {
      page.value = 1;
      animeStore.query = search_q.value;
      animeStore.getSearchedCharacter(page.value);
      search_q.value = "";
    };
    const ToCard = (itemId) => {
      router.push({
        name: "character",
        params: { id: itemId },
      });
      console.log(itemId);
    };
    onMounted(() => {
      animeStore.query = [];
      animeStore.getSearchedCharacter(page.value);
    });
    return {
      animeStore,
      GetSearched,
      ToCard,
      search_q,
      NextPage,
      PreviousPage,
      page,
    };
  },
};
</script>

<style lang="css" scoped>
.page {
  color: #7c7a7ab2;
  margin-top: 10px;
}
.pagination {
  display: flex;
  justify-content: center;
  margin-top: 20px;
  margin-right: 10px;
}
.next_page {
  margin-left: 10px;
  padding: 15px;
  position: relative;
  background: #7c7a7a;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.75);
}
.next_page span {
  position: relative;
  z-index: 1;
}
.next_page::after,
.next_page::before {
  content: "";
  position: absolute;
  right: -15px;
  top: 50%;
  background: #7c7a7a;
  width: 40px;
  height: 40px;
  margin-top: -20px;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.75);
  z-index: -1;
  transform: rotate(45deg);
}
.next_page::before {
  z-index: 1;
  box-shadow: none;
}
.previous_page {
  margin-right: 10px;
  position: relative;
  background: #7c7a7a;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.75);
}
.previous_page span {
  position: relative;
  z-index: 1;
}
.previous_page::after,
.previous_page::before {
  content: "";
  position: absolute;
  left: -15px;
  top: 50%;
  background: #7c7a7a;
  width: 40px;
  height: 40px;
  margin-top: -20px;
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.75);
  z-index: -1;
  transform: rotate(45deg);
}

.previous_page::before {
  z-index: 1;
  box-shadow: none;
}
.previous_page:hover,
.previous_page:hover:after,
.previous_page:hover:before {
  background: #0f3beb;
}
.next_page:hover,
.next_page:hover:after,
.next_page:hover:before {
  background: #0f3beb;
}
.header_search {
  line-height: 1.6;
  font-size: 1rem;
  margin-bottom: 30px;
}
.input {
  color: white;
  border-radius: 10px;
  width: 100%;
  height: 50px;
  font-size: 30px;
  padding-left: 20px;
  background-color: #1f1f1f;
}
.input:focus {
  border-color: white;
}
</style>
