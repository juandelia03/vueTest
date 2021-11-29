<template>
  <div class="product">
    <div class="image-wrap">
      <div class="left-arrow" @click="$emit('prev')">
        <img src="../assets/arrow.svg" alt="" />
      </div>
      <img :src="img" class="main-image" />
      <div class="right-arrow" @click="$emit('next')">
        <img src="../assets/arrow.svg" alt="" />
      </div>
    </div>
    <h3>{{ title }}</h3>
    <p class="price">${{ price }}</p>
    <Button content="ADD TO CART" @click="add" />
  </div>
</template>

<script>
import { inject } from "vue";
import Button from "./Button.vue";
export default {
  name: "Product",
  setup() {
    const store = inject("store");
    return {
      store,
    };
  },
  props: {
    title: String,
    price: String,
    img: String,
    hasDiscount: Boolean,
    discount: Number,
  },
  components: {
    Button,
  },
  methods: {
    add() {
      let itemsInCart = [];
      const item = { title: this.title, img: this.img };
      this.store.state.cart.forEach((e) => {
        itemsInCart.push(e.title);
      });
      if (itemsInCart.includes(item.title)) {
        return;
      } else {
        this.store.state.cart.push(item);
        localStorage.setItem("items", JSON.stringify(this.store.state.cart));
      }
    },
  },
};
</script>

<style scoped>
.product {
  max-width: 300px;
  margin-top: 20px;
  margin-right: 20px;
}
.image-wrap {
  width: 300px;
  height: 300px;
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid lightgray;
  padding: 10px;
}
.main-image {
  width: 100%;
}
.price {
  color: gray;
}
.right-arrow {
  display: none;
}
.left-arrow {
  display: none;
}
@media (max-width: 920px) {
  .left-arrow {
    margin-right: 30px;
    display: flex;
    transform: rotate(180deg);
  }
  .right-arrow {
    margin-left: 30px;
    display: flex;
  }
}
</style>
