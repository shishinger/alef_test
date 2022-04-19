<script setup>
import SuggestCard from "./SuggestCard.vue";
</script>
<template>
  <section>
    <ul class="suggestion">
      <suggest-card v-for="n in 5" :key="n" />
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.suggestion {
  width: 100%;
  display: grid;
  max-width: 1388px;
  -ms-grid-columns: 1fr 0.5fr 0.5fr;
  grid-template-columns: 1fr 0.5fr 0.5fr;
  -ms-grid-rows: calc(var(--2xl) * 10) calc(var(--2xl) * 10);
  grid-template-rows: calc(var(--2xl) * 10) calc(var(--2xl) * 10);
  grid-gap: var(--normal);
  @media (max-width: 1100px) {
    max-width: 100%;
    grid-template-columns: 1fr 1fr;
    -ms-grid-rows: 2fr 1fr 1fr;
    grid-template-rows: 2fr 1fr 1fr;
  }
}
</style>
