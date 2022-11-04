<template>
  <form class="search-bar-wrap">
    <input @keyup="findAnime" v-model="query" type="text" />
    <button @click.prevent="findAnime" type="submit">Search</button>
  </form>
</template>

<script>
export default {
  props: ["animelist"],
  emits: ["get-filtered-anime"],
  data() {
    return {
      query: "",
    };
  },
  methods: {
    findAnime() {
      if (this.query.length > 0) {
        const anime_list = this.animelist.filter((eachAnime) => {
          return eachAnime.heading
            .toUpperCase()
            .match(this.query.toUpperCase());
        });

        this.$emit("get-filtered-anime", anime_list, "clicked");
      } else {
        const anime_list = [];
        this.$emit("get-filtered-anime", anime_list, "empty");
      }
    },
  },
};
</script>

<style scoped>
* {
  outline: none;
}
.search-bar-wrap {
  width: 60%;
  margin: auto;
}
.search-bar-wrap > input {
  width: 50%;
  height: 32px;
  background-color: white;
  border: 1.3px solid #dfe1e6;
  border-radius: 5px;
}

.search-bar-wrap > button {
  height: 35px;
  margin: 0 10px;
  width: 100px;
  border: none;
  cursor: pointer;
  background-color: darkgrey;
  font-size: 1rem;
  border-radius: 5px;
}
</style>
