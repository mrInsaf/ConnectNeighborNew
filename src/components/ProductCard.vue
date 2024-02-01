<!-- ProductCard.vue -->

<template>
  <div class="product-card">
    <img :src="housing.imageSrc" alt="Product Image" class="product-image">

    <h2 class="product-price">{{ formattedPrice }}</h2>
    <p class="product-title">{{ housing.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    housing: Object,
    idx: Number,
    currentIndex: Number,
  },
  computed: {
    formattedPrice() {
      return `${this.housing.price} ₽`;
    },
  },
};
</script>

<style scoped>
/* Стили для компонента (scoped означает, что стили применяются только к данному компоненту) */
.product-card {
  width: fit-content;
  font-family: Arial, sans-serif;
  border: 1px solid #ccc;
  border-radius: 10px;
  margin-bottom: 16px;
  background-color: #fcfff0;
  position: relative;
}



.product-image {
  border-radius: 10px;
  max-width: 340px;
  height: auto;
  margin-bottom: 8px;
}

.product-title {
  font-size: 1.0em;
  margin-bottom: 8px;
  padding-left: 8px;
}

.product-price {
  padding-left: 8px;
  font-weight: bold;
}
</style>
