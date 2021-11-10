<template>
  <div class="button">
    <h5>{{ content }}</h5>
  </div>
</template>

<script>
export default {
  props: {
    content: String,
  },
};
</script>

<style>
.button {
  height: 50px;
  width: 60%;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border: black 1px solid;
}
.button h5 {
  color: white;
}
.button:hover {
  background: white;
}
.button:hover h5 {
  color: black;
}
</style>
