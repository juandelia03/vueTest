<template>
  <div class="wrap">
    <Header />
    <div class="sections">
      <div class="section">
        <h2>Best Sellers</h2>
        <div class="products">
          <Product
            v-for="product in products"
            :key="product.title"
            :title="product.title"
            :price="product.price"
            :img="product.img"
            :hasDiscount="product.hasDiscount"
            :discount="product.discount"
          />
        </div>
        <div class="products-mobile">
          <Product
            :key="products[product].title"
            :title="products[product].title"
            :price="products[product].price"
            :img="products[product].img"
            :hasDiscount="products[product].hasDiscount"
            :discount="products[product].discount"
            @prev="prev"
            @next="next"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import store from "../store";
import { provide } from "vue";
import Header from "./components/Header.vue";
import Product from "./components/Product.vue";
export default {
  name: "App",
  setup() {
    provide("store", store);
  },
  components: {
    Header,
    Product,
  },
  data() {
    return {
      products: [
        { title: "Mechanical keyboard", price: "1,122", img: require("@/assets/keyboard.jpg") },
        { title: "Headphones", price: "2,321", img: require("@/assets/headphones.jpg") },
        { title: "Mouse", price: "500", img: require("@/assets/mouse.jpg") },
        { title: "Web Cam", price: "300", img: require("@/assets/webcam.jpg") },
      ],
      product: 0,
    };
  },
  methods: {
    prev() {
      if (this.product !== 0) {
        this.product--;
      } else {
        this.product = this.products.length - 1;
      }
    },
    next() {
      if (this.product !== this.products.length - 1) {
        this.product++;
      } else {
        this.product = 0;
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
#app {
  min-height: 100vh;
  font-family: "Roboto", sans-serif;
  background-color: whitesmoke;
}
.wrap {
  padding: 10px 40px;
}
.sections {
  margin: 0px 12%;
}
.section {
  margin-top: 100px;
}
.products {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
@media (max-width: 920px) {
  .products {
    display: none;
  }
  .section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .products-mobile {
    display: flex;
  }
}
</style>
