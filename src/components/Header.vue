<template>
  <div class="hello">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1 {
    color: var(--primary-color);
    font-size: 25px;
    margin-bottom: 2rem;
  }
</style>
