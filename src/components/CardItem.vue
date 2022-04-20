<script setup>
import { ref } from "vue";
import ImageGallery from "./ImageGallery.vue";
import ModalAdd from "./ModalAdd.vue";

const title = ref("Пижама для девочек");
const amount = ref(1);
const rating = ref(4);
const place = ref("");
const sales = ["Скидка -36%", "Акция -20%"];
const sizes = ["Выбрать размер", "Выбрать размер", "Выбрать размер"];
const addedToCart = ref(false);

function addTo(where) {
  switch (where) {
    case "cart":
      place.value = "корзину";
      break;
    case "fav":
      place.value = "избранное";
    default:
      break;
  }
  addedToCart.value = true;
  setTimeout(() => (addedToCart.value = false), 5000);
}
</script>
<template>
  <section class="card">
    <image-gallery />
    <div class="card__info">
      <div class="card__about">
        <h2 class="title">{{ title }}</h2>
        <p class="article">Арт. 02765/46</p>
        <a href="javascript:void(0)" class="reviews">
          <h3 class="reviews__title">Отзывы</h3>
          <div
            class="stars"
            role="img"
            :aria-label="'Рейтинг: ' + rating"
            :alt="'Рейтинг: ' + rating"
          >
            <img
              src="../assets/stack.svg#star_full"
              v-for="fullStar in rating"
              :key="fullStar"
              width="10"
              height="10"
              aria-hidden="true"
              focusable="false"
              alt=""
            />
            <img
              src="../assets/stack.svg#star"
              v-for="empryStar in 5 - rating"
              :key="empryStar"
              width="10"
              height="10"
              aria-hidden="true"
              focusable="false"
              alt=""
            />
          </div>
          <span class="reviews__amount">14 отзывов</span>
          <img
            class="arrow"
            src="../assets/stack.svg#arrow"
            width="16"
            height="16"
            alt=""
          />
        </a>
      </div>
      <a href="javascript:void(0)" class="price">
        <div class="price__actual" title="Новая цена" aria-label="Новая цена">
          800 &#8381;
        </div>
        <div class="price__old" title="Cтарая цена" aria-label="Cтарая цена">
          1 500 &#8381;
        </div>
        <img
          class="arrow"
          src="../assets/stack.svg#arrow"
          width="16"
          height="16"
          alt=""
        />
        <div class="sale">
          <div class="sale__item" v-for="sale in sales" :key="sale">
            {{ sale }}
          </div>
        </div>
      </a>
      <div class="size">
        <div class="size__input">
          <select name="size" id="size" class="size__input">
            <option disabled>Выбрать размер</option>
            <option v-for="size in sizes" :key="size" :value="size">
              {{ size }}
            </option>
          </select>
          <label for="size" class="hidden">Выбрать размер</label>
        </div>
        <a href="javascript:void(0)" class="link">Определить размер</a>
      </div>
      <div class="add">
        <div class="add__counter">
          <button class="add__plus" @click="amount++">
            + <span class="hidden">Увеличить количество на 1 единицу</span>
          </button>
          <input
            type="number"
            name="amount"
            id="amount"
            class="add__amount"
            v-model.number="amount"
            min="1"
          />
          <label for="amount" class="hidden"
            >Количество товара {{ amount }} едениц</label
          >
          <button class="add__minus" @click="amount--">
            – <span class="hidden">Уменьшить количество на 1 единицу</span>
          </button>
        </div>
        <button class="to-cart" @click="addTo('cart')" :disabled="amount < 1">
          Добавить в корзину
        </button>
        <button class="to-fav" @click="addTo('fav')" :disabled="amount < 1">
          <img
            src="../assets/stack.svg#favorite"
            width="17"
            height="17"
            alt=""
            aria-hidden="true"
            focusable="false"
          />
          <span class="hidden">Добавить в избранное</span>
        </button>
        <a href="javascript:void(0)" class="link">Купить в 1 клик</a>
      </div>
      <ul class="card__desc">
        <li class="desc">
          <a href="javascript:void(0)" class="link">Описание товара</a>
        </li>
        <li class="shipping">
          <a href="javascript:void(0)" class="link">Доставка и возврат</a>
        </li>
        <li class="payment">
          <a href="javascript:void(0)" class="link">Способы оплаты</a>
        </li>
      </ul>
    </div>
    <a href="javascript:void(0)" class="link more">Посмотреть все стили</a>
  </section>
  <modal-add
    v-if="addedToCart"
    :class="{ js_fade: addedToCart }"
    :title="title"
    :amount="amount"
    :place="place"
  />
</template>

<style lang="scss" scoped>
.card {
  display: grid;
  -ms-grid-columns: repeat(2, 1fr);
  grid-template-columns: repeat(2, 1fr);
  @supports (column-gap: 10px) {
    column-gap: var(--normal);
  }
  &__about {
    padding: var(--xl) var(--large);
  }
  &__desc {
    display: flex;
    flex-direction: column;
    row-gap: var(--small);
    padding: var(--big);
  }
  @media (max-width: 750px) {
    display: flex;
    flex-direction: column;
  }
}
.title {
  margin-bottom: calc(var(--xs) / 3);
  font-weight: 600;
  font-size: 18px;
  line-height: var(--lh_bg);
}
.article {
  margin-bottom: var(--large);
  font-size: var(--small);
  line-height: var(--lh_bg);
  letter-spacing: var(--ls);
  color: var(--accent_dark);
}
.reviews {
  display: flex;
  align-items: baseline;
  &__title {
    margin-right: var(--small);
    font-size: var(--normal);
    font-weight: 400;
    line-height: var(--lh_lg);
    letter-spacing: var(--ls);
  }
  &__amount {
    position: relative;
    line-height: var(--lh_lg);
    letter-spacing: var(--ls);
  }
  .arrow {
    transition: transform 0.2s ease;
  }
  @media (hover: hover) {
    &:hover .arrow {
      transform: translate(50%, 0px) scale(1.2);
    }
  }
  &:active {
    color: var(--accent_dark);
  }
}
.stars {
  display: flex;
  margin-right: calc(var(--xs) / 2);
  @supports (column-gap: 2px) {
    column-gap: 2px;
  }
}
.price {
  display: flex;
  align-items: baseline;
  flex-wrap: wrap;
  padding: var(--large);
  letter-spacing: var(--ls);
  @supports (column-gap: 14px) {
    column-gap: var(--normal);
  }
  &__actual {
    font-weight: 700;
    font-size: var(--xl);
    line-height: var(--lh_nm);
  }
  &__old {
    position: relative;
    line-height: var(--lh_lg);
    text-decoration: line-through;
    color: var(--accent_dark);
  }
  .arrow {
    transition: transform 0.2s ease;
  }
  @media (hover: hover) {
    &:hover .arrow {
      transform: translate(50%, 0px) scale(1.2);
    }
  }
  &:active {
    color: var(--accent_dark);
  }
}
.sale {
  display: flex;
  flex: 0 0 100%;
  margin-top: var(--small);
  @supports (column-gap: 10px) {
    column-gap: var(--xs);
  }
  &__item {
    width: max-content;
    padding: calc(var(--xs) / 2.5) calc(var(--normal) / 2);
    font-size: var(--small);
    line-height: var(--lh_bg);
    border: 1px solid var(--text);
    text-transform: lowercase;
  }
}
.size {
  display: flex;
  flex-direction: column;
  row-gap: var(--small);
  padding: var(--small) var(--large);
  &__input {
    position: relative;
    width: 100%;
    max-width: calc(var(--2xl) * 10);
    transition: var(--shadow_animation);
    @media (hover: hover) {
      &:hover {
        box-shadow: var(--box-shadow_active) var(--shadow_blue);
      }
    }
    select {
      -webkit-appearance: none;
      appearance: none;
      padding: var(--xs) var(--xs);
      font-size: var(--normal);
      line-height: var(--lh_bg);
      letter-spacing: var(--ls);
      border: 1px solid var(--text);
      color: var(--text);
    }
    &::after {
      content: "";
      position: absolute;
      width: var(--normal);
      height: var(--normal);
      top: 50%;
      right: var(--xs);
      background-image: url("../assets/stack.svg#arrow");
      transform: rotate(90deg) translate(-50%, 50%);
    }
  }
}
.link {
  width: max-content;
  line-height: var(--lh_bg);
  text-decoration: underline;
  letter-spacing: var(--ls);
  transition: color 0.1s var(--sine), text-decoration-color 0.3s var(--sine);
  @media (hover: hover) {
    &:hover {
      text-decoration-color: transparent;
    }
  }
  &:active {
    color: var(--blue);
  }
}
.add {
  display: flex;
  align-items: stretch;
  flex-wrap: wrap;
  padding: var(--2xl) 0 var(--2xl) var(--xl);
  border-bottom: 0.5px solid var(--accent_light);
  &__plus,
  &__minus,
  &__amount {
    text-align: center;
    color: var(--text);
  }
  &__plus,
  &__minus {
    width: calc(var(--large) * 2);
    height: calc(var(--large) * 2);
    transition: var(--shadow_animation), transform 0.15s ease;
    @media (hover: hover) {
      &:hover {
        box-shadow: var(--box-shadow_hover) var(--shadow_blue);
      }
    }
    &:active {
      transform: translateY(2px);
      box-shadow: var(--box-shadow_active) var(--shadow_blue);
    }
  }
  &__amount {
    width: calc(var(--2xl) * 1.7);
    padding: var(--xs) 0;
    -webkit-appearance: textfield;
    appearance: textfield;
    &:invalid {
      outline: 1px solid var(--error);
    }
  }
  .link {
    flex: 0 0 100%;
    margin-top: var(--xs);
  }
  @media (max-width: 950px) {
    flex-wrap: wrap;
    row-gap: var(--midi);
    &__counter {
      flex: 0 0 100%;
    }
  }
}
.to-cart,
.to-fav {
  letter-spacing: var(--ls);
  color: var(--bg);
  background-color: var(--text);
  text-align: center;
  transition: var(--shadow_animation), transform 0.15s ease;
  @media (hover: hover) {
    &:not(:disabled):hover {
      box-shadow: var(--box-shadow_hover) var(--shadow_blue);
    }
  }
  &:not(:disabled):active {
    transform: translateY(2px);
    box-shadow: var(--box-shadow_active) var(--shadow_blue);
  }
  &:disabled {
    background-color: var(--accent_dark);
  }
}
.to-cart {
  margin-left: var(--small);
  padding: var(--small) calc(var(--normal) * 2);
  @media (max-width: 950px) {
    margin-left: 0;
  }
}
.to-fav {
  color: var(--bg);
  padding: var(--normal);
  margin-left: calc(var(--small) / 2);
  img {
    filter: invert(100%);
  }
}
.desc,
.shipping,
.payment {
  display: flex;
  align-items: center;
  line-height: var(--lh_lg);
  @supports (column-gap: 10px) {
    column-gap: var(--xs);
  }
  &::before {
    width: var(--midi);
    height: var(--midi);
  }
}
.desc::before {
  content: url("../assets/stack.svg#closes");
}
.shipping::before {
  content: url("../assets/stack.svg#clock");
}
.payment::before {
  height: var(--xs);
  content: url("../assets/stack.svg#pay");
}
.more {
  grid-column: span 2;
  margin: var(--2xl) auto;
  text-align: center;
}
</style>
