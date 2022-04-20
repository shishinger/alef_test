<script setup>
import { ref } from "vue";

const bigImg = ref([
  new URL("../assets/sleepwear1.jpg", import.meta.url).href,
  new URL("../assets/sleepwear1-2x.jpg", import.meta.url).href,
]);
function getImg(img) {
  return [
    new URL(`../assets/sleepwear${img}.jpg`, import.meta.url).href,
    new URL(`../assets/sleepwear${img}-2x.jpg`, import.meta.url).href,
  ];
}
</script>
<template>
  <div class="gallery">
    <img
      :src="bigImg[0]"
      :srcset="bigImg[1] + ' 2x'"
      class="gallery__main-img"
      alt="Изображение товара"
    />
    <ul class="gallery__list">
      <li
        class="gallery__item"
        v-for="imageNumber in 5"
        :key="imageNumber"
        @click="bigImg = getImg(imageNumber)"
        @keyup.enter="bigImg = getImg(imageNumber)"
        tabindex="0"
      ></li>
    </ul>
  </div>
</template>

<style lang="scss">
.gallery {
  position: relative;
  &__list {
    position: absolute;
    top: var(--xl);
    left: var(--xl);
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 10%;
    row-gap: var(--xs);
    z-index: 1;
  }
  @supports (aspect-ratio: 1 / 1.28) {
    &__main-img {
      aspect-ratio: 1 / 1.28;
    }
  }
  @supports (aspect-ratio: 1 / 1.28) {
    &__item {
      aspect-ratio: 0.769 / 1;
    }
  }
  &__item {
    position: relative;
    transition: transform 0.2s ease;
    cursor: pointer;
    background-repeat: no-repeat;
    background-size: cover;
    @for $i from 1 through 5 {
      &:nth-child(#{$i}) {
        background-image: url("../assets/thumb#{$i}.jpg");
      }
    }
    &::before {
      position: absolute;
      content: "";
      top: 0;
      left: 0;
      display: block;
      width: 100%;
      height: 100%;
      background-color: var(--bg);
      opacity: 0.3;
      transition: opacity 0.2s ease;
    }
    @media (hover: hover) {
      &:hover {
        transform: scale(1.1);
        &::before {
          opacity: 0;
        }
      }
    }
  }
}
</style>
