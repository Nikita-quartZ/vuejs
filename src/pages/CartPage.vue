<template>
  <main class="content container">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="index.html">
            Каталог
          </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link">
            Корзина
          </a>
        </li>
      </ul>

      <h1 class="content__title">
        Корзина
      </h1>
      <span class="content__info">
        {{ products.length }} {{ changeWord(products.length) }}
      </span>
    </div>

    <section class="cart">
      <form class="cart__form form" action="#" method="POST">
        <div class="cart__field">
          <ul class="cart__list">
            <CartItem :item="item" v-for="item in products" :key="item.productId" />
          </ul>
        </div>

        <div class="cart__block">
          <p class="cart__desc">
            Мы&nbsp;посчитаем стоимость доставки на&nbsp;следующем этапе
          </p>
          <p class="cart__price">
            Итого: <span>{{ totalPrice }} ₽</span>
          </p>

          <button class="cart__button button button--primery" type="submit">
            Оформить заказ
          </button>
        </div>
      </form>
    </section>
  </main>
</template>

<script>
import { mapGetters } from 'vuex';
import CartItem from '../components/CartItem.vue';

export default {
  computed: {
    ...mapGetters({products: 'cartDetailsProduct', totalPrice: 'cartTotalPrice'}),
  },
  methods: {
    changeWord(number) {
      let amount = number % 100;
      let wordForBar;
      if (amount <= 20) {
        if (amount === 0 || (amount > 4 && amount <= 20)) {
          wordForBar = "товаров";
        } else if (amount === 1) {
          wordForBar = "товар";
        } else if (amount > 1 && amount < 5) {
          wordForBar = "товара";
        }
      } else {
        amount = amount % 10;
        if (amount === 0 || (amount > 4 && amount <= 9)) {
          wordForBar = "товаров";
        } else if (amount === 1) {
          wordForBar = "товар";
        } else if (amount > 1 && amount < 5) {
          wordForBar = "товара";
        }
      }
      return wordForBar
    },
  },
  components: {
    CartItem,
  }
}
</script>