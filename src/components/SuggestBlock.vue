<script setup>
import SuggestCard from "./SuggestCard.vue";
</script>
<template>
  <section class="suggest">
    <ul class="suggest__list">
      <suggest-card v-for="n in 5" :key="n" />
    </ul>
  </section>
</template>

<style lang="scss" scoped>
.suggest {
  width: 100%;
  display: grid;
  min-width: 0;
  max-width: 1388px;
  grid-template-columns: minmax(0, 1fr) minmax(0, 0.5fr) minmax(0, 0.5fr);
  grid-auto-columns: min-content;
  grid-template-rows: calc(var(--2xl) * 10) calc(var(--2xl) * 10);
  grid-gap: var(--normal);
  &__list {
    display: contents;
  }
  @media (max-width: 1100px) {
    & {
      max-width: 100%;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 2fr 1fr 1fr;
    }
  }
}
</style>
