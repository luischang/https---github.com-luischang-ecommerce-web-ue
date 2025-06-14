<template>
  <h5>Listado de Productos</h5>
  <div class="product-list">
    <div class="product-grid">
      <div class="product-item" v-for="item in filteredProducts" :key="item.id">
        <q-img
          :src="item.imageUrl"
          alt="Product Image"
          class="product-image"
          style="width: 100%; height: auto"
        />
        <h6>{{ item.description }}</h6>
        <p>Precio: {{ item.price }}</p>
      </div>
    </div>
  </div>
</template>
<style>
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
</style>

<script>
export default {
  name: 'ProductList',
  computed: {
    filteredProducts() {
      console.log('Categoria filtrada:', this.categoriaFiltrada)
      return this.products.filter((product) => {
        console.log('Filtering product:', product)
        if (!this.categoriaFiltrada) {
          console.log('No category filter applied, returning all products')
          return true // No filter applied, return all products
        }
        return product.categoryId === this.categoriaFiltrada
      })
    },
  },
  data() {
    return {
      products: [],
    }
  },
  props: {
    categoriaFiltrada: {
      type: Object,
      default: null,
    },
  },
  methods: {
    loadProducts() {
      // Simulate an API call to fetch products
      // this.products = [
      //   { id: 1, name: 'Product 1', price: 100 },
      //   { id: 2, name: 'Product 2', price: 200 },
      //   { id: 3, name: 'Product 3', price: 300 },
      // ]
      let token = localStorage.getItem('token')

      this.$api
        .get('/api/products', {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          console.log(response)
          this.products = response.data
        })
    },
  },
  mounted() {
    this.loadProducts()
  },
}
</script>
