<template>
  <section>
    <div class="card-content-wrap">
      <img class="class-img" :src="require(`../assets/${imagelink}`)" />
      <div class="anime-details">
        <h4>{{ heading }}</h4>
        <p>{{ truncateString }}</p>
      </div>
    </div>
    <div v-if="list_type === 'my_anime'" class="anime-watch-count-wrap">
      <button
        class="anime-watch-count-button"
        @click="updateEpisodeCount('inc', id)"
        type="button"
      >
        +
      </button>
      <p>{{ currentEpisode }} / {{ episodeCount }}</p>
      <button
        class="anime-watch-count-button"
        @click="updateEpisodeCount('dec', id)"
        type="button"
      >
        -
      </button>
    </div>
    <div v-else class="anime-watch-add-wrap">
      <button
        :disabled="getDisabledStatus"
        class="anime-watch-add-button"
        type="button"
        @click="addAnimeToList"
      >
        Add to my Anime List
      </button>
    </div>
  </section>
  <!-- <button class="add-to-anime" type="button">ADD TO MY ANIME</button> -->
</template>

<script>
export default {
  props: [
    "animelist",
    "id",
    "imagelink",
    "alttext",
    "heading",
    "paragraph",
    "episodeCount",
    "currentEpisode",
    "list_type",
  ],
  emits: ["add-anime-to-my-list"],

  data() {
    return {
      isDisabled: false,
    };
  },
  methods: {
    updateEpisodeCount(incdec, id) {
      if (incdec === "inc") {
        this.$emit("update-episode-count", "inc", id);
      } else if (incdec === "dec") {
        this.$emit("update-episode-count", "dec", id);
      }
    },
    addAnimeToList() {
      const current_anime = {
        id: this.id,
        imagelink: this.imagelink,
        alttext: this.alttext,
        heading: this.heading,
        paragraph: this.paragraph,
        episode_count: this.episodeCount,
        current_episode: this.currentEpisode,
      };
      this.$emit("add-anime-to-my-list", current_anime);
    },
  },
  computed: {
    truncateString() {
      if (this.paragraph.length < 400) {
        return this.paragraph;
      }
      return this.paragraph.substring(0, 400);
    },
    getDisabledStatus() {
      const isInList = this.animelist.find(
        (eachAnime) => eachAnime.id === this.id
      );
      console.log(isInList);
      return isInList;
    },
  },
};
</script>

<style scoped>
section {
  position: relative;
}
.card-content-wrap {
  display: flex;
  justify-content: space-between;
}

.class-img {
  height: 150px;
  width: 120px;
  border-radius: 10px;
  margin-right: 20px;
}

.anime-details {
  flex: 3;
  text-align: left;
}

.add-to-anime {
  height: 20px;
  float: right;
  /* margin: -20px 0; */
  cursor: pointer;
}

.anime-watch-count-wrap {
  display: flex;
  justify-content: end;
  align-items: center;
  position: absolute;
  top: 70%;
  left: 67%;
}

.anime-watch-count-button {
  width: 50px;
  height: 30px;
  cursor: pointer;
  margin: 0 20px;
}

.anime-watch-add-wrap {
  display: flex;
  justify-content: end;
}
.anime-watch-add-button {
  height: 30px;
  cursor: pointer;
}
</style>
