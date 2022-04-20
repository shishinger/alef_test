<script setup>
import { ref } from "vue";
import CardItem from "./components/CardItem.vue";
import MainFooter from "./components/MainFooter.vue";
import MainHeader from "./components/MainHeader.vue";
import SuggestBlock from "./components/SuggestBlock.vue";

const isOut = ref(false);

document.addEventListener("scroll", function () {
  let scrollPrev = 0;
  let scrolled = document.documentElement.scrollTop;
  if (scrolled > 100 && scrolled > scrollPrev) {
    isOut.value = true;
  } else {
    isOut.value = false;
  }
  scrollPrev = scrolled;
});
</script>

<template>
  <main-header :class="{ js_out: isOut }" />
  <main class="main">
    <h1 class="hidden">Тестовое задание Alef</h1>
    <card-item />
    <suggest-block />
  </main>
  <main-footer />
</template>

<style lang="scss">
@import "./assets/reset.scss";
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap");
:root {
  --text: #333333;
  --bg: #f2f2f2;
  --accent_dark: #828282;
  --accent_light: #c4c4c4;
  --error: #e0514a;
  --blue: rgba(51, 51, 255, 0.8);
  --shadow_dark: rgba(0, 0, 0, 0.1);
  --shadow_blue: rgba(51, 51, 255, 0.26);
  --centering: calc((100% - 1385px) / 2);
  --xs: 0.7em;
  --small: 0.857em;
  --normal: 1em;
  --midi: 1.143em;
  --big: 1.428em;
  --large: 1.571em;
  --xl: 1.71em;
  --2xl: 2.357em;
  --lh_nm: 1;
  --lh_bg: 1.33;
  --lh_lg: 1.43;
  --ls: 0.04em;
  --bottom-line: 0px 2px 4px 0;
  --box-shadow_hover: 2px 2px 10px 0;
  --box-shadow_active: 2px 2px 0 0;
  --shadow_animation: box-shadow 0.25s ease-in-out;
  --sine: cubic-bezier(0.45, 0.05, 0.55, 0.95);
}
:focus {
  outline: 1px solid var(--shadow_blue);
  outline-offset: 2px;
}
:focus:not(:focus-visible) {
  outline: none;
}
:focus-visible {
  outline: 2px solid #a5c9ff;
  outline-offset: 2px;
}
html {
  font-size: 14px;
  background-color: var(--bg);
  color: var(--text);
  font-family: "Open Sans", sans-serif;
}
body {
  background-color: inherit;
}
.main {
  position: relative;
  margin: 66px auto 0;
  width: 100%;
  max-width: 1390px;
}
section {
  overflow-x: hidden;
}
.js_out {
  transform: translateY(-100%);
}
</style>
