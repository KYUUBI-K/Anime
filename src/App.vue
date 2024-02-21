<template>
  <div class="app">
    <div class="wrapper">
      <header class="header">
        <div class="header_inner">
          <div class="header_menu">
            <ul class="header_navbar">
              <li>
                <router-link class="nav_link" to="/">Home</router-link>
              </li>
              <li>
                <router-link class="nav_link" to="/animes"
                  >Anime list</router-link
                >
              </li>

              <li>
                <router-link class="nav_link" to="/characters"
                  >Heroes</router-link
                >
              </li>

              <li>
                <router-link class="nav_link" to="/genres">genres</router-link>
              </li>
              <li>
                <router-link
                  @click="RandomAnime()"
                  class="nav_link"
                  to="/randomAnime"
                  >unpredictable</router-link
                >
              </li>
            </ul>
            <!-- <search-block /> -->
          </div>
        </div>
      </header>
      <div class="content">
        <router-view></router-view>
      </div>

      <footer class="footer">
        <div class="about">
          <router-link class="nav_about" to="/about">About us</router-link>
        </div>
      </footer>
    </div>
  </div>
</template>
<script>
import SearchBlock from "@/components/SearchBlock";
import { useAnimeStore } from "@/stores/animes";

export default {
  components: {
    SearchBlock,
  },
  setup() {
    const animeStore = useAnimeStore();
    const RandomAnime = () => {
      animeStore.getRandomAnime();
    };
    return { animeStore, RandomAnime };
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  outline: none;
  border: 0;
  box-sizing: border-box;
}
body {
  font: 1.3rem "Roboto", sans-serif;
  background: #141414;
  /* padding-top: 200px; */
  position: relative;

  color: #fff;
}
.wrapper {
  margin: 0 auto;
  background: #141414;
  padding: 0 30px;
}
.header {
  font: 1.6rem "Roboto", sans-serif;
  background-color: #1f1f1f;
  color: #fff;
  margin: 0 -30px;
  padding: 15px 30px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
  position: sticky;
  top: 0;
  z-index: 100;
}
.header_inner {
  margin: 0 auto;
  position: relative;
  z-index: 20;
  align-items: center;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  color: #fff;
  justify-content: center;
}
/*  */
.header_menu {
  text-transform: uppercase;
  display: flex;
}
a {
  color: #fff;
  text-decoration: none;
}
.nav_link {
  padding: 0.6rem 1rem;
  text-decoration: none;
}
.nav_link:hover {
  color: #0f3beb;
}
.header_navbar {
  margin-right: 150px;
  display: flex;
}

li {
  list-style-type: none;
}
.content {
  margin-top: 20px;
  padding: 1rem;
  min-height: 780px;
}
.footer {
  color: #7c7a7a;
  font: 1.6rem "Roboto", sans-serif;

  background-color: #1f1f1f;
  margin: 0 -30px;
  padding: 15px 30px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  position: static;
}
.footer_anipedia {
  /* color: #7c7a7a; */
}
.nav_about {
  color: #7c7a7a;
  text-decoration: none;
}
.nav_about:hover {
  color: #fff;
}
</style>
