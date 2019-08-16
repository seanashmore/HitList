<template>
  <div>
    <nav class="navbar navbar-expand-md navbar-light bg-light">
      <a href="#" class="navbar-brand">HitList</a>

      <button
        type="button"
        class="navbar-toggler"
        data-toggle="collapse"
        data-target="#navbarCollapse"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarCollapse">
        <div class="navbar-nav">
          <a v-on:click="lastWeek" href="#" class="nav-item nav-link">Last Week</a>
          <a v-on:click="thisWeek" href="#" class="nav-item nav-link">This Week</a>
          <a v-on:click="nextWeek" href="#" class="nav-item nav-link">Next Week</a>
          <input v-model="query" v-on:change="searchChanged" type="text" name="search" value="">
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import axios from "axios";
import { EventBus } from "../js/event-bus.js";

export default {
  data() {
    return {
      query: ''
    }
  },
  methods: {
    searchChanged: function() {
      console.log('query = ' + this.query)
    },
    thisWeek: function() {
      axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://api.shortboxed.com/comics/v1/new"
        )
        .then(response => {
          console.log(response["data"]);
          EventBus.$emit('this-week-received', response["data"]);
        });
    }, 
    lastWeek: function() {
      axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://api.shortboxed.com/comics/v1/previous"
        )
        .then(response => {
          console.log(response["data"]);
          EventBus.$emit('last-week-received', response["data"]);
        });
    },
    nextWeek: function() {
      axios
        .get(
          "https://cors-anywhere.herokuapp.com/https://api.shortboxed.com/comics/v1/future"
        )
        .then(response => {
          console.log(response["data"]);
          EventBus.$emit('next-week-received', response["data"]);
        });
    }            
  }
};
</script>

<style>
</style>
