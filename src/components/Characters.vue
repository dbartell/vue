<template>
  <Character v-for="(character, index) in characters" :key="index" :character="character" />
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