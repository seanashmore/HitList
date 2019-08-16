<template>
  <div>
    <ul>
      <li v-for="comic in comicsList" :key="comic.diamond_id">
        <p>
          <strong>{{comic.title}}</strong>
          <br />
          <small>{{comic.description}}</small>
        </p>
      </li>
    </ul>
  </div>
</template>

<script>
import { EventBus } from "../js/event-bus.js";

export default {
  data() {
    return {
      comicsList: ""
    };
  },
  created() {
    EventBus.$on("this-week-received", data => {
      this.setComics(data["comics"]);
    });

    EventBus.$on("last-week-received", data => {
      this.setComics(data["comics"]);
    });

    EventBus.$on("next-week-received", data => {
      this.setComics(data["comics"]);
    });

    EventBus.$on("filter-on-search", query => {
      this.comicsList = comicsList.filter(function(query) {
        return comic.title === query
      });
      console.log('New comicsList -> ' + comicsList)
    });
  },
  methods: {
    setComics(comics) {
      console.log("setComics called");
      this.comicsList = comics;
    }
  }
};
</script>

<style>
</style>
