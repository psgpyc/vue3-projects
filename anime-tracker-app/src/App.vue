<template>
  <h2>Anime Tracker</h2>
  <search-bar
    :animelist="full_anime_list"
    @get-filtered-anime="displayFilteredAnime"
  ></search-bar>
  <h3 v-if="!displayFilteredCard" class="header-anime">My Anime</h3>
  <h3 v-if="displayFilteredCard">Filtered Anime List</h3>
  <card-layout v-if="!displayFilteredCard">
    <each-card v-for="anime in anime_list" :key="anime.id"
      ><card-contents
        :id="anime.id"
        :imagelink="anime.imagelink"
        :alttext="anime.alttext"
        :heading="anime.heading"
        :paragraph="anime.paragraph"
        :episodeCount="anime.episode_count"
        :currentEpisode="anime.current_episode"
        @update-episode-count="updateEpisodeCount"
        list_type="my_anime"
      ></card-contents
    ></each-card>
  </card-layout>
  <card-layout v-if="displayFilteredCard">
    <each-card v-for="anime in filtered_anime_list" :key="anime.id"
      ><card-contents
        :animelist="anime_list"
        :id="anime.id"
        :imagelink="anime.imagelink"
        :alttext="anime.alttext"
        :heading="anime.heading"
        :paragraph="anime.paragraph"
        :episodeCount="anime.episode_count"
        :currentEpisode="anime.current_episode"
        @add-anime-to-my-list="addAnimeToList"
        list_type="filtered_anime"
      ></card-contents
    ></each-card>
  </card-layout>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import CardLayout from "./components/CardLayout.vue";
import EachCard from "./components/EachCard.vue";
import CardContents from "./components/CardContents.vue";

export default {
  components: { SearchBar, CardLayout, EachCard, CardContents },
  data() {
    return {
      anime_list: [
        {
          id: 0,
          imagelink: "naruto.jpg",
          alttext: "naruto anime",
          heading: "Naruto Shippuden",
          paragraph:
            "Naruto, an adolescent ninja, dreams of becoming the Hokage in his village.",
          episode_count: 220,
          current_episode: 0,
        },
        {
          id: 1,
          imagelink: "onepiece.jpg",
          alttext: "one piece anime",
          heading: "One Piece",
          paragraph:
            "One Piece is a Japanese manga series written and illustrated by Eiichiro Oda. ",
          episode_count: 220,
          current_episode: 0,
        },
      ],
      full_anime_list: [
        {
          id: 0,
          imagelink: "naruto.jpg",
          alttext: "naruto anime",
          heading: "Naruto Shippuden",
          paragraph:
            "Naruto, an adolescent ninja, dreams of becoming the Hokage in his village.",
          episode_count: 220,
          current_episode: 0,
        },
        {
          id: 1,
          imagelink: "onepiece.jpg",
          alttext: "one piece anime",
          heading: "One Piece",
          paragraph:
            "One Piece is a Japanese manga series written and illustrated by Eiichiro Oda. ",
          episode_count: 220,
          current_episode: 0,
        },
        {
          id: 3,
          imagelink: "attackontitans.jpg",
          alttext: "attackontitan anime",
          heading: "Attack On Titan",
          paragraph:
            "When man-eating Titans first appeared 100 years ago, humans found safety behind massive walls that stopped the giants in their tracks. ",
          episode_count: 220,
          current_episode: 0,
        },
      ],

      displayFilteredCard: false,
      filtered_anime_list: null,
    };
  },
  methods: {
    updateEpisodeCount(incdec, id) {
      const get_anime = this.anime_list.find(
        (each_anime) => each_anime.id === id
      );
      if (incdec === "inc") {
        get_anime.current_episode < get_anime.episode_count
          ? get_anime.current_episode++
          : get_anime.episode_count;
      } else if (incdec === "dec") {
        get_anime.current_episode > 0 ? get_anime.current_episode-- : 0;
      }
    },
    displayFilteredAnime(filtered_anime_list, click_val) {
      if (click_val === "clicked") {
        this.displayFilteredCard = true;

        this.filtered_anime_list = filtered_anime_list;
      }
      if (click_val === "empty") {
        this.displayFilteredCard = false;
      }
      // console.log(filtered_anime_list);
    },
    addAnimeToList(anime_to_be_added) {
      this.displayFilteredCard = false;

      this.anime_list.push(anime_to_be_added);
    },
  },
  computed: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.header-anime {
  margin: 50px;
}
</style>
