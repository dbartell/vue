<template>
  
  <img v-bind:src="character.image.medium" />
  {{ character.name }}
  {{ character.playedBy[0] }}
</template>

<script>
import Character from './Character.vue';

export default {
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
};
</script>
