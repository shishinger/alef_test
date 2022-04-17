<script setup>
import { ref } from "vue";

const isTouched = ref(false);
</script>
<template>
  <li class="suggestion__card" @touchend="isTouched = !isTouched">
    <div class="suggestion__hint" :class="{ open: isTouched }">
      <p>Узнай, что на мне</p>
      <div class="suggestion__likes">200</div>
    </div>
    <a
      href="javascript:void(0)"
      class="full-link"
      title="Предлагаемый товар"
      @focusin="isTouched = !isTouched"
      @focusout="isTouched = !isTouched"
    ></a>
  </li>
</template>
<style lang="scss" scoped>
.suggestion {
  &__card {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    color: var(--bg);
    &:nth-of-type(1) {
      grid-row: span 2;
    }
    @for $i from 1 through 5 {
      &:nth-child(#{$i}) {
        background-image: url("../assets/suggest#{$i}.jpg");
      }
    }
    & .full-link:focus {
      &__hint {
        opacity: 1;
      }
    }
    @media (max-width: 1100px) {
      aspect-ratio: 1 / 1;
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
    transition: 0.4s ease;
    &::before {
      content: "";
      width: 10%;
      height: 12%;
      margin-bottom: var(--xs);
      background-image: url("../assets/stack.svg#bag_suggest");
    }
    &::after {
      content: "";
      position: absolute;
      top: 5%;
      right: 0;
      width: 10%;
      height: 12%;
      background-image: url("../assets/stack.svg#full_screen");
    }
  }
  &__likes {
    position: absolute;
    bottom: 0;
    display: flex;
    align-items: center;
    column-gap: var(--xs);
    transform: translateY(-100%);
    &::before {
      content: "";
      width: var(--midi);
      height: var(--midi);
      background-image: url("../assets/stack.svg#favorite_full");
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
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
.open {
  opacity: 1;
}
</style>
