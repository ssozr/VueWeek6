<template>
  <table class="table">
    <tbody>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.title }}</td>
        <td><img :src="product.imageUrl" width="200" alt=""></td>
        <td>{{ product.price }}</td>
        <td><RouterLink :to="`/product/${product.id}`">產品詳細資訊</RouterLink></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import { RouterLink } from 'vue-router'
const { VITE_APP_URL, VIRE_APP_PATH } = import.meta.env

export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getProducts () {
      this.$http.get(`${VITE_APP_URL}/v2/api/${VIRE_APP_PATH}/products/all`)
        .then((res) => {
          this.products = res.data.products
        })
        .catch((err) => {
          console.log(err)
        })
    }
  },
  components: {
    RouterLink
  },
  mounted () {
    this.getProducts()
  }
}
</script>
