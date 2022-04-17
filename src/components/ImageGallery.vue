<script setup>
import { ref } from "vue";

const bigImg = ref(new URL("../assets/sleepwear1.jpg", import.meta.url).href);
function getImg(img) {
  return new URL(`../assets/sleepwear${img}.jpg`, import.meta.url).href;
}
</script>
<template>
  <div class="gallery">
    <img :src="bigImg" class="gallery__main-img" alt="" />
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
    max-width: calc(var(--2xl) * 2);
    max-width: 10%;
    row-gap: var(--xs);
    z-index: 1;
  }
  &__main-img {
    aspect-ratio: 1 / 1.28;
  }
  &__item {
    position: relative;
    aspect-ratio: 0.769 / 1;
    cursor: pointer;
    @for $i from 1 through 5 {
      &:nth-child(#{$i}) {
        background-repeat: no-repeat;
        background-size: cover;
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
      transition: 0.2s ease;
    }
    &:hover {
      &::before {
        opacity: 0;
      }
    }
    &_curent::before {
      opacity: 0;
    }
  }
}
</style>
