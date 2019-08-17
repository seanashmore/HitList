<template>
  <div>
    <ul>
      <br />
      <li v-for="comic in filteredComicsList" :key="comic.diamond_id">
        <p>
          <strong>{{comic.title}}</strong>
          <template v-if="comic.description !== ''">
            <br />
            <small>{{comic.description}}</small>
          </template>
          <br />
          <small><b>Published by:</b> {{ comic.publisher }}</small>
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
      comicsList: [],
      filteredComicsList: []
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
      console.log('Received filter-on-search with query: ' + query)
      this.filteredComicsList = this.comicsList.filter(function(comic) {
        console.log('This comic title -> ' + comic.title)
        return comic.title.toLowerCase().includes(query.toLowerCase())
      });
    });
  },
  methods: {
    setComics(comics) {
      console.log("setComics called");
      this.comicsList = comics;
      this.filteredComicsList = comics;
    }
  }
};
</script>

<style>
</style>
