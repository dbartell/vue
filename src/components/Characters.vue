<template>
<div
    class="characters"
  >
    <Character v-for="(character, index) in characters" :key="index" :character="character" />
  </div>
</template>

<script>
  import Character from './Character.vue';

  export default {
    props: {
      characters: {
        type: Array,
        required: true,
      }
    },
    components: {
      Character,
    },
  }
</script>

<style>
  .characters {
    display: grid;
    grid-template-rows: 1fr;
    grid-template-columns: 350px;
    justify-content: center;
  }
</style>