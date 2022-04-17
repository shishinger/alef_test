<script setup>
import { ref } from "vue";

const headerService = {
  Аккаунт: "person",
  Избранное: "favorite",
  Корзина: "bag",
};
const menu = [
  "Постельное белье",
  "Одежда для дома",
  "Одежда для улицы",
  "Выход",
];
const isOpen = ref(false);

function getImg(img) {
  return new URL(`../assets/stack.svg#${img}`, import.meta.url).href;
}
</script>
<template>
  <header class="header">
    <p class="logo"><a href="javascript:void(0)">Logo</a></p>
    <ul class="service">
      <li
        class="service__item"
        v-for="(iconId, btnLabel) in headerService"
        :key="iconId"
      >
        <button class="service__btn" :title="btnLabel">
          <img
            :src="getImg(iconId)"
            width="16"
            height="16"
            alt=""
            aria-hidden="true"
          />
          <span class="hidden">{{ btnLabel }}</span>
        </button>
      </li>
      <li class="service__item menu">
        <button
          :class="{ cross: isOpen }"
          class="service__btn menu__btn"
          title="Меню"
          @click="isOpen = !isOpen"
        >
          <div class="menu__item" v-for="n in 3" :key="n"></div>
          <span class="hidden">Меню</span>
        </button>
      </li>
    </ul>
    <nav :class="{ open: isOpen }" class="nav">
      <ul class="nav__list">
        <li class="nav__item" v-for="menuItem in menu" :key="menuItem">
          <a href="javascript:void(0)" tabindex="-1">{{ menuItem }}</a>
        </li>
      </ul>
    </nav>
    <div
      :class="{ open: isOpen }"
      class="overlay"
      @click="isOpen = !isOpen"
    ></div>
  </header>
</template>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  padding: var(--xs) var(--centering);
  box-shadow: var(--bottom-line);
  background-color: var(--bg);
  transition: transform 0.2s ease;
  z-index: 2;
  @media (max-width: 1390px) {
    --centering: var(--big);
  }
}
.logo {
  font-weight: 700;
  font-size: var(--large);
  line-height: var(--lh_nm);
  text-transform: uppercase;
  letter-spacing: var(--ls);
}
.service {
  display: flex;
  align-items: center;
  column-gap: var(--xl);
  border: 1px solid transparent;
  &__item {
    position: relative;
    transition: opacity 0.2s ease-in-out;
    &::before {
      content: "";
      position: absolute;
      inset: 95% 0% 0 0%;
      background-color: var(--text);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.4s ease-in-out;
      z-index: -1;
    }
    &:active {
      opacity: 0.5;
    }
    &:hover::before,
    &:active::before {
      transform: scaleX(1);
      transform-origin: left;
    }
  }
  &__btn {
    padding: 4px;
    color: var(--text);
  }
}
.menu {
  z-index: 2;
  &__btn {
    display: flex;
    flex-direction: column;
    row-gap: calc(var(--xs) / 2);
  }
  &__item {
    width: var(--midi);
    height: 1px;
    background-color: var(--text);
    display: flex;
    transition: transform 0.2s cubic-bezier(0.68, -0.55, 0.27, 1.55);
    .cross &:nth-of-type(1) {
      transform: rotate(45deg) translateX(1px);
    }
    .cross &:nth-of-type(2) {
      opacity: 0;
    }
    .cross &:nth-of-type(3) {
      transform: rotate(135deg) translateX(-1px);
    }
  }
  @media (min-width: 751px) {
    display: none;
  }
}
.cross {
  row-gap: 0;
  z-index: 2;
}
.nav {
  position: absolute;
  top: 0;
  left: 0;
  padding: calc(var(--2xl) * 2) var(--2xl) var(--large);
  width: 100%;
  background-color: var(--bg);
  font-size: var(-small);
  line-height: var(--lh_bg);
  letter-spacing: var(--ls);
  text-transform: uppercase;
  transform: translateY(-100%);
  transition: transform 0.4s ease-in;
  z-index: 1;
  &__list {
    display: flex;
    flex-direction: column;
    row-gap: var(--2xl);
  }
}

.out {
  transform: translateY(-100%);
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 0;
  transform: translateY(-200%);
  background-color: transparent;
  pointer-events: all;
}
.open {
  transform: translateY(0);
}
</style>
