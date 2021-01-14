<template>
  <div id="app">
    <header>
      <div class="title">{{ title }}</div>
    </header>

    <section class="main-content w-50 mx-auto">
      <ul class="nav nav-tabs">
        <li class="nav-item" v-for="tab in tabs" :key="tab" @click="selected = tab;">
          <a class="nav-link" v-bind:class="{ active: isActive(tab) }" href="#">{{ tab }}</a>
        </li>
      </ul>
      <component :is="selected"></component>
    </section>
  </div>
</template>

<script>
import WindowsList from './components/WindowsList.vue';
import RoomsList from "./components/RoomsList";
import RoomNew from "./components/RoomNew";
import WindowNew from "./components/WindowNew";

export default {
  name: 'App',
  components: {
    WindowsList,
    RoomsList,
    RoomNew,
    WindowNew
  },
  data: function () {
    return {
      title: 'Faircorp',
      tabs: ['WindowsList', 'RoomsList', 'RoomNew', 'WindowNew'],
      selected: 'WindowsList'
    }
  },
  methods: {
    isActive(tab) {
      return tab === this.selected
    }
  }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
