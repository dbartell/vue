<template>
  <div id="app">
    <Header title="Game of Thrones Character Search"/>
    <SearchInput aria-label="Search" v-on:keyup="fetchCharacter($event)" v-model="search"/>
    <Characters v-if="!loading && !error" :characters="results">
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from "axios";

import Header from './components/Header.vue';
import SearchInput from 'vue-search-input';
import Characters from './components/Characters.vue';

export default {
  name: 'App',
  components: {
    Header,
    SearchInput,
    Characters,
  },
  data() {
    return {
      search: '',
      results: [],
      loading: false,
      error: null
    }
  },
  methods: {
    async fetchCharacter() {
      
      try {
        this.loading = false;
        this.error = null;
        const url = `https://www.anapioficeandfire.com/api/characters?name=${this.search}`;
        const { data } = await axios.get(url);
        this.results = data;
        console.log(this.results)
      } catch(err) {
        console.error(err)
      }
    }
  }
}
</script>

<style>
@import 'vue-search-input/dist/styles.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
