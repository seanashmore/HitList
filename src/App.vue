<template>
  <div>
    <nav-menu></nav-menu>
    <comic-list></comic-list>
  </div>
</template>

<script>
import BootstrapCard from "./components/BootstrapCard.vue";
import NavMenu from "./components/NavMenu.vue";
import ComicList from "./components/ComicList.vue";
import { EventBus } from "./js/event-bus.js";

export default {
  components: { BootstrapCard, NavMenu, ComicList }
};
</script>

<style lang="scss">
</style>
