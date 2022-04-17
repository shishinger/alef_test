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
  <main-header :class="{ out: isOut }" />
  <main class="main">
    <card-item />
    <suggest-block />
  </main>
  <main-footer />
</template>

<style lang="scss">
@import "./assets/reset.scss";
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap");
:root {
  // colors
  --text: #333333;
  --bg: #f2f2f2;
  --accent_dark: #828282;
  --accent_light: #c4c4c4;
  --bottom-line: 0px 2px 4px rgba(0, 0, 0, 0.1);
  // sizes
  --centering: calc((100% - 1385px) / 2);
  --xs: 0.7em; //10px
  --small: 0.857em; //12px
  --normal: 1em; //14px
  --midi: 1.143em; //16px
  --big: 1.428em; //20px
  --large: 1.571em; //22px
  --xl: 1.71em; //24px
  --2xl: 2.357em; //33px
  // line height
  --lh_nm: 1;
  --lh_bg: 1.33;
  --lh_lg: 1.43;
  // letter spasing
  --ls: 0.04em;
  // media queries
  --big-screen: 1390px;
}
:focus {
  outline: 1px solid #a5c9ff;
}
body {
  font-size: 14px;
  background-color: var(--bg);
  color: var(--text);
  font-family: "Open Sans", sans-serif;
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
.full-link {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  border: 0;
  padding: 0;
  white-space: nowrap;
  clip-path: inset(100%);
  clip: rect(0 0 0 0);
  overflow: hidden;
}
</style>
