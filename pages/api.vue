<template>
  <nuxt-content :document="doc" />
</template>

<script lang="ts">
import {
  defineComponent,
  useContext,
  useAsync,
  onServerPrefetch,
  computed,
  onMounted
} from "nuxt-composition-api";

export default defineComponent({
  setup() {
    const { $content, params } = useContext();
    const fetchContent = () => {
      return $content(params.value.slug || "index").fetch();
    };

    const doc = useAsync(fetchContent);
    onServerPrefetch(async () => {
      doc.value = await fetchContent();
    });

    return {
      doc
    };
  }
});
</script>