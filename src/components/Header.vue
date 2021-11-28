<template>
  <div>
    <div class="header">
      <h2>Marketplace</h2>
      <div class="cart-wrap" @click="openCart">
        <img src="../../src/assets/cart.png" alt="" />
      </div>
    </div>
    <div class="cart-content" v-if="isOpened">
      <div class="box">
        <CartItem
          v-for="item in store.state.cart"
          :key="item"
          :title="item.title"
          :img="item.img"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
import CartItem from "./cartItem.vue";
export default {
  components: { CartItem },
  name: "Header",
  setup() {
    const store = inject("store");
    return {
      store,
    };
  },
  data() {
    return {
      isOpened: false,
    };
  },
  methods: {
    openCart() {
      this.isOpened = !this.isOpened;
    },
  },
  mounted() {
    if (localStorage.items) {
      this.store.state.cart = JSON.parse(localStorage.items);
    }
  },
};
</script>

<style>
.cart-wrap img {
  width: 30px;
  height: 30px;
  cursor: pointer;
}
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.cart-content {
  position: absolute;
  right: 20px;
  width: 100%;
  display: flex;
  justify-content: flex-end;
}
.box {
  overflow: scroll;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: white;
  height: 500px;
  width: 400px;
  border-radius: 50px;
  border: solid 1px lightgray;
}
.box::-webkit-scrollbar {
  display: none;
}
</style>
