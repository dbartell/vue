<template>
  <div
    v-on:click="isOpen = !isOpen"
    class="mt-2 bg-pallblue text-white p-4 font-bold rounded cursor-pointer"
  >
    <div class="flex justify-between">
      {{ heading }}

      <ChevronDownIcon
        class="-mr-1 ml-2 h-5 w-5"
        f
        aria-hidden="true"
        v-if="!isOpen"
      />

      <ChevronUpIcon
        class="-mr-1 ml-2 h-5 w-5"
        aria-hidden="true"
        v-else="isOpen"
      />
    </div>
  </div>
  <div class="border p-2 text-left" :class="isOpen ? 'd-block' : 'hidden'">
    <slot></slot>
  </div>
</template>
<script>
import { ChevronDownIcon, ChevronUpIcon } from '@heroicons/vue/solid';
export default {
  data: () => {
    return {
      isOpen: false,
    };
  },
  name: 'Accordion',
  props: {
    heading: String,
  },
  components: {
    ChevronDownIcon,
    ChevronUpIcon,
  },
};
</script>
