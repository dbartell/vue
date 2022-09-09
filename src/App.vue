<template>
  <div id="app">
    <Header title="Game of Thrones Character Search"/>
    <SearchInput aria-label="Search" v-on:keyup="fetchCharacter($event)" v-model="search"/>
    <Characters v-if="!loading && !error" :characters="results">
  </div>
</template>

<script>
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
      cast: [],
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
        const charactersPlusCastInformation = data.map(character => {
          const foundCastInformation = this.cast.find(castMember => castMember.character.name.includes(character.name));
          return (foundCastInformation)
            ? {...character, ...foundCastInformation.character}
            : character;
        })
        this.results = charactersPlusCastInformation;
      } catch(err) {
        console.error(err)
      }
    },
    async getCastInformation() {
      try{
        const url = `https://api.tvmaze.com/shows/82?embed=cast`;
        const { data } = await axios.get(url);
        this.cast = data._embedded.cast;
      } catch(err) {
        console.error(err);
      }
    },
  },
  created() {
    this.getCastInformation()
  },
}
</script>

<style>
@import 'vue-search-input/dist/styles.css';

#app {
  --primary-color: #42b883;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
