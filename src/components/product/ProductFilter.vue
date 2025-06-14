<template>
  <h6>Filtros</h6>
  <div class="category-filter">
    <q-select
      v-model="selectedCategory"
      :options="categories"
      option-label="description"
      option-value="id"
      label="Select Category"
      emit-value
      map-options
      filled
    />
  </div>
</template>
<script>
export default {
  name: 'ProductFilter',
  data() {
    return {
      categories: [],
      selectedCategory: null,
    }
  },
  methods: {
    loadCategories() {
      // Simulate an API call to fetch categories
      //   this.categories = [
      //     { id: 1, name: 'Electronics' },
      //     { id: 2, name: 'Books' },
      //     { id: 3, name: 'Clothing' },
      //   ]
      //Get token from localStorage
      let token = localStorage.getItem('token')

      this.$api
        .get('/api/categories', {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        })
        .then((response) => {
          console.log(response)
          this.categories = response.data
        })
    },
  },
  mounted() {
    this.loadCategories()
  },
}
</script>
