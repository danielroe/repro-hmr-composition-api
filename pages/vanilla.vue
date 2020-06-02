<template>
  <nuxt-content :document="doc" />
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  data: () => ({
    doc: null
  }),
  async asyncData({ $content }) {
    return { doc: await $content("index").fetch() };
  }
});
</script>