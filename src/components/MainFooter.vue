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
      <fieldset class="field" alt="Форма подписки">
        <div class="field__input">
          <input
            type="email"
            name="email"
            id="email"
            class="email"
            v-model="emailValue"
            placeholder="Адрес электронной почты"
            autocomplete="email"
            aria-invalid="true"
            aria-describedby="email_error"
          />
          <p class="email__error" id="email_error">Введите корректный адрес</p>
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
  margin: calc(var(--normal) * 11) 0 calc(var(--2xl) * 2);
  display: grid;
  -ms-grid-columns: 0.7fr 0.7fr 1fr;
  grid-template-columns: 0.7fr 0.7fr 1fr;
  padding: 0 calc(var(--2xl) * 4.1);
  @supports (column-gap: 38px) {
    column-gap: var(--2xl);
  }
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
    line-height: var(--lh_lg);
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
    &:active {
      color: var(--blue);
      &::before {
        background-color: currentColor;
      }
    }
  }
  @media (max-width: 950px) {
    display: flex;
    flex-wrap: wrap;
    row-gap: var(--2xl);
    padding: var(--big);
    margin: var(--2xl) auto;
    &__title {
      max-width: 60%;
    }
  }
}
.field {
  display: flex;
  flex-wrap: wrap;
  row-gap: var(--2xl);
  &__input {
    position: relative;
    flex: 0 0 100%;
  }
}
.email {
  position: relative;
  margin-top: var(--normal);
  width: 100%;
  padding: var(--small) var(--midi);
  font-size: var(--normal);
  line-height: var(--large);
  letter-spacing: var(--ls);
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
  top: 50%;
  transform: translate(-80%, 0);
  background-image: url("../assets/stack.svg#close");
  transition: filter 0.3s ease-in-out;
  @media (hover: hover) {
    &:hover {
      filter: brightness(0);
    }
  }
  &:active {
    box-shadow: var(--box-shadow_active) var(--shadow_blue);
  }
}
.subscribe {
  padding: calc(var(--midi) / 2) calc(2 * var(--normal));
  font-size: var(--normal);
  line-height: var(--lh_lg);
  letter-spacing: var(--ls);
  border: 1px solid var(--text);
  margin-left: auto;
  transition: var(--shadow_animation);
  @media (hover: hover) {
    &:hover {
      box-shadow: var(--box-shadow_hover) var(--shadow_blue);
    }
  }
  &:active {
    box-shadow: var(--box-shadow_active) var(--shadow_blue);
  }
}
</style>
