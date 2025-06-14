<template>
  <div class="product-page">
    <div class="product-filter q-ml-md q-mr-xl">
      <ProductFilter @categoryChanged="updateProductCategory" />
    </div>
    <div class="product-list">
      <ProductList :categoriaFiltrada="categorySelected" />
    </div>
  </div>
</template>

<style>
.product-page {
  display: flex;
  justify-content: space-between;
}
.product-filter {
  width: 25%;
}

.product-list {
  width: 75%;
}
</style>
<script>
import ProductFilter from 'src/components/product/ProductFilter.vue'
import ProductList from 'src/components/product/ProductList.vue'
export default {
  name: 'ProductPage',
  components: {
    ProductFilter,
    ProductList,
  },
  data() {
    return {
      // You can add any data properties you need here
      categorySelected: null,
    }
  },
  methods: {
    updateProductCategory(category) {
      // Handle the category change event from ProductFilter
      console.log('Selected category:', category)
      // You can implement logic to filter products based on the selected category
      this.categorySelected = category
    },
  },
}
</script>
