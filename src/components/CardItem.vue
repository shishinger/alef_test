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
          <div class="stars" :title="'Рейтинг: ' + rating">
            <img
              src="../assets/stack.svg#star_full"
              v-for="fullStar in rating"
              :key="fullStar"
              width="10"
              height="10"
              alt=""
            />
            <img
              src="../assets/stack.svg#star"
              v-for="empryStar in 5 - rating"
              :key="empryStar"
              width="10"
              height="10"
              alt=""
            />
          </div>
          <span class="reviews__amount">14 отзывов</span>
        </a>
      </div>

      <a class="price">
        <div class="price__actual">800 &#8381;</div>
        <div class="price__old">1 500 &#8381;</div>
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
            <option v-for="size in sizes" :key="size">{{ size }}</option>
          </select>
          <label for="size" class="hidden">Выбрать размер</label>
        </div>
        <a href="javascript:void(0)" class="link">Определить размер</a>
      </div>
      <div class="add">
        <div class="add__counter">
          <button class="add__plus" @click="amount++">+</button>
          <input
            type="number"
            name="amount"
            id="amount"
            class="add__amount"
            v-model.number="amount"
            min="1"
          />
          <label for="amount" class="hidden">Количество товара</label>
          <button class="add__minus" @click="amount--">–</button>
        </div>
        <button class="to-cart" @click="addTo('cart')">
          Добавить в корзину
        </button>
        <button class="to-fav" @click="addTo('fav')">
          <img
            src="../assets/stack.svg#favorite"
            width="16"
            height="15"
            alt=""
          />
          <span class="hidden">Добавить в избранное</span>
        </button>
        <a href="javascript:void(0)" class="link">Купить в 1 клик</a>
      </div>
      <div class="card__desc">
        <a href="javascript:void(0)" class="link desc">Описание товара</a>
        <a href="javascript:void(0)" class="link shipping"
          >Доставка и возврат</a
        >
        <a href="javascript:void(0)" class="link payment">Способы оплаты</a>
      </div>
    </div>
    <a href="javascript:void(0)" class="link more">Посмотреть все стили</a>
  </section>
  <modal-add
    v-if="addedToCart"
    :class="{ fade: addedToCart }"
    :title="title"
    :amount="amount"
    :place="place"
  />
</template>

<style lang="scss" scoped>
.card {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  font-size: var(--normal);
  &__info {
    padding: var(--xl) var(--2xl);
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
  &__about {
    margin-bottom: calc(var(--2xl) * 1.4);
  }
  &__desc {
    display: flex;
    flex-direction: column;
    row-gap: var(--xs);
  }
  @media (max-width: 750px) {
    display: flex;
    flex-direction: column;
  }
}
.title {
  margin-bottom: var(--xs);
  font-weight: 600;
  font-size: 18px;
  line-height: var(--lh_nm);
}
.article {
  margin-bottom: var(--large);
  font-size: var(--small);
  line-height: var(--lh_nm);
  letter-spacing: var(--ls);
  color: var(--accent_dark);
}
.reviews {
  display: flex;
  align-items: baseline;
  position: relative;
  width: max-content;
  &__title {
    margin-right: var(--normal);
    font-size: var(--normal);
    font-weight: 400;
    line-height: var(--lh_bg);
    letter-spacing: var(--ls);
  }
  &__amount {
    position: relative;
    &::after {
      content: url("../assets/stack.svg#arrow");
      position: absolute;
      width: var(--normal);
      height: var(--normal);
      transform: translateX(100%);
      transition: transform 0.2s ease-in-out;
    }
  }
  &:hover &__amount::after {
    transform: translateX(100%) scale(1.5);
  }
  &:active {
    color: var(--accent_dark);
  }
}
.stars {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-right: calc(var(--xs) / 2);
}
.price {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  column-gap: var(--normal);
  margin-bottom: var(--2xl);
  letter-spacing: var(--ls);
  &__actual {
    font-weight: 700;
    font-size: var(--xl);
    line-height: var(--lh_nm);
  }
  &__old {
    position: relative;
    font-size: var(--normal);
    line-height: var(--lh_bg);
    text-decoration: line-through;
    color: var(--text);
    &::after {
      content: url("../assets/stack.svg#arrow");
      position: absolute;
      width: var(--normal);
      height: var(--normal);
      transform: translateX(100%);
      transition: transform 0.2s ease-in-out;
    }
  }
  &:hover &__old::after {
    transform: translateX(100%) scale(1.5);
  }
  &:active {
    color: var(--accent_dark);
  }
}
.sale {
  display: flex;
  column-gap: calc(var(--xs) / 2);
  flex: 0 0 100%;
  margin-top: var(--small);
  &__item {
    width: max-content;
    padding: calc(var(--xs) / 2) var(--xs);
    font-size: var(--small);
    line-height: var(--lh_bg);
    letter-spacing: var(--ls);
    border: 1px solid var(--text);
    text-transform: lowercase;
  }
}
.size {
  display: flex;
  flex-direction: column;
  row-gap: var(--small);
  margin-bottom: calc(var(--2xl) * 1.3);
  &__input {
    position: relative;
    width: 100%;
    max-width: calc(var(--2xl) * 10);
    select {
      appearance: none;
      width: 100%;
      padding: var(--xs);
      font-size: var(--normal);
      line-height: var(--lh_bg);
      letter-spacing: var(--ls);
      border: 1px solid var(--text);
    }
    &::after {
      content: "";
      position: absolute;
      display: inline-block;
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
  font-size: var(--normal);
  line-height: var(--lh_bg);
  text-decoration: underline;
  letter-spacing: var(--ls);
  transition: text-decoration-color 0.2s ease;
  &:hover {
    text-decoration-color: #993366;
  }
  &:active {
    color: #993366;
  }
}
.add {
  display: flex;
  align-items: stretch;
  flex-wrap: wrap;
  margin-bottom: var(--xl);
  padding-bottom: var(--2xl);
  border-bottom: 0.5px solid var(--accent_light);
  &__plus,
  &__minus,
  &__amount {
    font-size: var(--normal);
    line-height: var(--lh_lg);
    letter-spacing: var(--ls);
  }
  &__plus,
  &__minus {
    width: calc(var(--large) * 2);
    height: calc(var(--large) * 2);
  }
  &__amount {
    width: calc(var(--2xl) * 2);
    appearance: textfield;
    text-align: center;
    &:invalid {
      outline: 1px solid red;
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
  font-size: var(--normal);
  line-height: var(--lh_bg);
  letter-spacing: var(--ls);
  color: var(--bg);
  background-color: var(--text);
  font-weight: 400;
  text-align: center;
  transition: box-shadow 0.4s ease;
  &:hover {
    box-shadow: 1px 4px 8px 0px rgba(51, 51, 51, 0.3);
  }
  &:active {
    box-shadow: 1px 4px 0px 0px rgba(51, 51, 51, 0.3);
  }
}
.to-cart {
  margin-left: var(--small);
  padding: var(--small) var(--xl);
  @media (max-width: 950px) {
    margin-left: 0;
  }
}
.to-fav {
  color: var(--bg);
  padding: var(--normal);
  margin-left: var(--xs);
  img {
    filter: invert(100%);
  }
}
.desc,
.shipping,
.payment {
  display: flex;
  column-gap: var(--xs);
  align-items: center;
  line-height: var(--large);
}
.desc::before {
  content: "";
  display: flex;
  width: var(--midi);
  height: var(--midi);
  background-image: url("../assets/stack.svg#closes");
}
.shipping::before {
  content: "";
  display: flex;
  width: var(--midi);
  height: var(--midi);
  background-position: center;
  background-size: cover;
  background-image: url("../assets/stack.svg#clock");
}
.payment::before {
  content: "";
  display: flex;
  width: var(--normal);
  height: var(--xs);
  background-image: url("../assets/stack.svg#pay");
}
.more {
  grid-column: span 2;
  margin: var(--2xl) auto;
  text-align: center;
}
</style>
