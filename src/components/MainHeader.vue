<script setup>
import { ref } from "vue";

const menu = [
  "Постельное белье",
  "Одежда для дома",
  "Одежда для улицы",
  "Выход",
];
const isOpen = ref(false);
</script>
<template>
  <header class="header">
    <p class="logo"><a href="javascript:void(0)">Logo</a></p>
    <ul class="service">
      <li class="service__item">
        <button class="service__btn" title="Аккаунт">
          <img
            src="../assets/stack.svg#person"
            width="16"
            height="16"
            alt=""
            aria-hidden="true"
            focusable="false"
          />
          <span class="hidden">Аккаунт</span>
        </button>
      </li>
      <li class="service__item">
        <button class="service__btn" title="Избранное">
          <img
            src="../assets/stack.svg#favorite"
            width="16"
            height="16"
            alt=""
            aria-hidden="true"
            focusable="false"
          />
          <span class="hidden">Избранное</span>
        </button>
      </li>
      <li class="service__item">
        <button class="service__btn" title="Корзина">
          <img
            src="../assets/stack.svg#bag"
            width="16"
            height="16"
            alt=""
            aria-hidden="true"
            focusable="false"
          />
          <span class="hidden">Корзина</span>
        </button>
      </li>
      <li class="service__item menu">
        <button
          :class="{ js_cross: isOpen }"
          class="service__btn menu__btn"
          title="Меню"
          aria-label="Меню"
          @click="isOpen = !isOpen"
        >
          <div class="menu__item" v-for="n in 3" :key="n"></div>
          <span class="hidden">Меню</span>
        </button>
      </li>
    </ul>
    <nav :class="{ js_open: isOpen }" class="nav">
      <ul class="nav__list">
        <li class="nav__item" v-for="menuItem in menu" :key="menuItem">
          <a href="javascript:void(0)" :tabindex="isOpen ? 0 : -1">
            {{ menuItem }}
          </a>
        </li>
      </ul>
    </nav>
    <div
      :class="{ js_open: isOpen }"
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
  box-shadow: var(--bottom-line) var(--shadow_dark);
  background-color: var(--bg);
  transition: transform 0.5s ease;
  z-index: 2;
  @media (max-width: 1390px) {
    padding: var(--big);
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
  align-items: flex-start;
  @supports (column-gap: 16px) {
    column-gap: var(--xl);
  }
  &__item {
    position: relative;
    transition: opacity 0.2s ease;
    &:not(.menu):before {
      content: "";
      position: absolute;
      inset: 95% 0 0 0;
      background-color: var(--text);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.4s ease-in-out;
      z-index: -1;
    }
    @media (hover: hover) {
      &:hover::before {
        transform: scaleX(1);
        transform-origin: left;
      }
    }
    &:active,
    &:active::before {
      opacity: 0.5;
    }
    &:active::before {
      transform: scaleX(1);
      transform-origin: left;
    }
  }
  &__btn {
    padding: 4px;
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
    transition: transform 0.3s cubic-bezier(0.68, -0.55, 0.27, 1.55),
      opacity 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55);
    .js_cross &:nth-of-type(1) {
      transform: rotate(45deg) translateX(1px);
    }
    .js_cross &:nth-of-type(2) {
      transform: translateX(100%);
      opacity: 0;
    }
    .js_cross &:nth-of-type(3) {
      transform: rotate(135deg) translateX(-1px);
    }
  }
  @media (min-width: 751px) {
    display: none;
  }
}
.js_cross {
  row-gap: 0;
}
.nav {
  position: absolute;
  top: 0;
  left: 0;
  padding: calc(var(--2xl) * 3) var(--2xl) calc(var(--xl) * 2);
  width: 100%;
  background-color: var(--bg);
  font-size: var(--small);
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
  &__item {
    position: relative;
    width: max-content;
    transition: opacity 0.2s ease-in-out;
    &::before {
      content: "";
      position: absolute;
      inset: 95% 0 0 0;
      background-color: var(--text);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.4s ease-in-out;
      z-index: -1;
    }
    @media (hover: hover) {
      &:hover::before {
        transform: scaleX(1);
        transform-origin: left;
      }
    }
    &:active,
    &:active::before {
      opacity: 0.5;
    }
    &:active::before {
      transform: scaleX(1);
      transform-origin: left;
    }
  }
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
.js_open {
  transform: translateY(0);
}
</style>
