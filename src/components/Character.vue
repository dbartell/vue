<template>
  <div class="character-card">
    <img v-if="character.image" v-bind:src="character.image.medium" v-bind:alt="character.name" />
    <img v-if="!character.image" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTSfeMmNmH7N8ri8eedtz2o2XJco5FG-BnghB7u7Mw&s" alt="Couldn't find profile picture" />
    <div class="character-card__info">
      <p>Name: <span>{{ character.name }}</span></p>
      <p>Played By: <span>{{ character.playedBy[0] }}</span></p>
      <p>Born: <span>{{ character.born }}</span></p>
      <p v-if="character.culture">Culture: <span>{{ character.culture }}</span></p>
    </div>
    <Accordion heading="Allegiences">
      <p v-for="allegiance in character.allegiances">{{allegiance}}</p>
    </Accordion>
  </div>
</template>

<script>
import Accordion from './Accordion.vue';
export default {
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
  components: {
    Accordion
  },
  created() {
    console.log(this.character)
  }
};
</script>

<style>
  .character-card {
    display: flex;
    flex-direction: column;
    margin: 2rem auto;
    width: 100%;
  }
  .character-card img {
    margin-bottom: 1rem;
  }
  .character-card p {
    text-align: left;
  }
  .character-card span {
    color: var(--primary-color);
    text-align: left;
  }
</style>
