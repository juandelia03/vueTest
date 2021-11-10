<template>
  <div class="item">
    <p>{{ title }}</p>
    <img :src="img" alt="" class="image" />
    <img src="../assets/delete.png" alt="" class="dlt" @click="dlt" />
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  name: "cartItem",
  setup() {
    const store = inject("store");
    return {
      store,
    };
  },
  props: {
    title: String,
    img: String,
  },
  methods: {
    dlt() {
      this.store.state.cart.forEach((e, i) => {
        if (e.title == this.title) {
          this.store.state.cart.splice(i, 1);
        }
      });

      //   this.store.state.cart.splice(i, 1);
    },
  },
};
</script>

<style scoped>
.item {
  width: 100%;
  display: flex;
  gap: 10px;
  align-items: center;
  border-bottom: 1px solid lightgray;
  padding: 20px;
  margin-left: 25px;
}
.image {
  width: 100px;
}
.dlt {
  width: 32px;
  cursor: pointer;
  margin-left: auto;
  margin-right: 30px;
}
</style>
