<script setup>
import { ref } from "vue";

const isTouched = ref(false);
const likes = ref(200);
</script>
<template>
  <li class="suggestion__card" @touchend="isTouched = !isTouched">
    <div class="suggestion__hint" :class="{ js_open: isTouched }">
      <p>Узнай, что на мне</p>
      <div class="suggestion__likes" :aria-label="likes + ' лайков'">
        {{ likes }}
      </div>
    </div>
    <a
      href="javascript:void(0)"
      class="full-link"
      title="Предлагаемый товар"
      aria-label="Предлагаемый товар"
      @focusin="isTouched = !isTouched"
      @focusout="isTouched = !isTouched"
    ></a>
  </li>
</template>
<style lang="scss" scoped>
.suggestion {
  &__card {
    position: relative;
    background-repeat: no-repeat;
    background-size: cover;
    color: var(--bg);
    &:nth-of-type(1) {
      grid-row: span 2;
    }
    @for $i from 1 through 5 {
      &:nth-child(#{$i}) {
        background-image: url("../assets/suggest#{$i}.jpg");
        @media (min-resolution: 1.5dppx) {
          background-image: url("../assets/suggest#{$i}-2x.jpg");
        }
      }
    }
    @media (max-width: 1100px) {
      @supports (aspect-ratio: 1 / 1) {
        aspect-ratio: 1 / 1;
      }
      &:nth-of-type(1) {
        grid-row: auto;
        grid-column: span 2;
      }
    }
  }
  &__hint {
    opacity: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background-color: rgb(51, 51, 51, 0.7);
    transition: opacity 0.4s ease;
    &::before,
    &::after {
      content: "";
      width: 10%;
      height: 11%;
      background-size: contain;
      background-repeat: no-repeat;
    }
    &::before {
      margin-bottom: var(--xs);
      background-image: url("../assets/stack.svg#bag_suggest");
    }
    &::after {
      content: "";
      position: absolute;
      top: 5%;
      right: 5%;
      width: 6%;
      height: 5%;
      background-image: url("../assets/stack.svg#full_screen");
    }
  }
  &__likes {
    position: absolute;
    bottom: 0;
    display: flex;
    align-items: center;
    transform: translateY(-100%);
    @supports (column-gap: 10px) {
      column-gap: var(--xs);
    }
    &::before {
      content: "";
      width: var(--normal);
      height: var(--midi);
      background-size: contain;
      background-repeat: no-repeat;
      background-image: url("../assets/stack.svg#favorite_full");
    }
  }
}
@media (hover: hover) {
  .suggestion__card:hover {
    .suggestion__hint {
      opacity: 1;
    }
  }
}
.js_open {
  opacity: 1;
}
.full-link {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
