<script setup>
import { ref } from "vue";

const emailValue = ref("");
</script>
<template>
  <footer class="footer">
    <ul class="footer__list">
      <li class="footer__title">Покупателям</li>
      <li class="footer__item"><a href="javascript:void(0)">Каталог</a></li>
      <li class="footer__item"><a href="javascript:void(0)">Акции</a></li>
      <li class="footer__item"><a href="javascript:void(0)">Бренды</a></li>
    </ul>
    <ul class="footer__list">
      <li class="footer__title">О нас</li>
      <li class="footer__item"><a href="javascript:void(0)">О компании</a></li>
      <li class="footer__item"><a href="javascript:void(0)">Новости</a></li>
      <li class="footer__item"><a href="javascript:void(0)">Команда</a></li>
    </ul>
    <div class="footer__list">
      <div class="footer__title">Узнайте первыми о новинках и акциях</div>
      <fieldset class="field">
        <div class="field__input">
          <input
            type="email"
            name="email"
            id="email"
            class="email"
            v-model="emailValue"
            placeholder="Адрес электронной почты"
          />
          <p class="email__error">Введите корректный адрес</p>
          <label for="email" class="hidden">Адрес электронной почты</label>
          <button class="reset" @click="emailValue = ''">
            <span class="hidden">Стереть email</span>
          </button>
        </div>
        <button type="submit" class="subscribe">Подписаться</button>
      </fieldset>
    </div>
  </footer>
</template>
<style lang="scss" scoped>
.footer {
  margin-top: calc(var(--normal) * 11);
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 0px calc(var(--2xl) * 4.1) calc(var(--2xl) * 2);
  &__list {
    display: flex;
    flex-direction: column;
    row-gap: 8px;
  }
  &__title,
  &__item {
    letter-spacing: var(--ls);
  }
  &__title {
    margin-bottom: var(--xs);
    font-size: var(--midi);
    line-height: 1.5;
    text-transform: uppercase;
  }
  &__item {
    position: relative;
    width: max-content;
    font-size: var(--normal);
    line-height: var(--lh_bg);
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
    @media (hover: hover) {
      &:hover::before {
        transform: scaleX(1);
        transform-origin: left;
      }
    }
  }
  @media (max-width: 950px) {
    display: flex;
    flex-wrap: wrap;
    row-gap: var(--2xl);
  }
}
.field {
  display: flex;
  flex-wrap: wrap;
  row-gap: calc(var(--xl) * 2);
  &__input {
    position: relative;
    flex: 0 0 100%;
    width: 100%;
  }
}
.email {
  position: relative;
  flex: 0 0 100%;
  width: 100%;
  padding: var(--small) var(--normal);
  font-size: var(--normal);
  line-height: var(--large);
  letter-spacing: var(--lh);
  border-bottom: 1px solid var(--accent_light);
  &__error {
    position: absolute;
    font-size: var(--xs);
    color: red;
    opacity: 0;
  }
  &:invalid {
    outline: 1px solid red;
    & + .email__error {
      opacity: 1;
    }
  }
}
.reset {
  position: absolute;
  width: var(--normal);
  height: var(--normal);
  right: 0;
  transform: translate(-100%, 100%);
  background-image: url("../assets/stack.svg#close");
}
.subscribe {
  padding: var(--xs) calc(2 * var(--normal));
  font-size: var(--normal);
  line-height: var(--lh_lg);
  letter-spacing: var(--ls);
  border: 1px solid var(--text);
  margin-left: auto;
}
</style>
