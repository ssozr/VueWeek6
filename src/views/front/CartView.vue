<template>
  <table class="table">
    <thead>
      <tr>
        <td>產品名稱</td>
        <td>數量</td>
        <td>價格</td>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in products" :key="item.id">
        <td>
          {{ item.product.title }}
        </td>
        <td>
          {{ item.qty }}
        </td>
        <td>
          {{ item.total }}
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>

const { VITE_APP_URL, VIRE_APP_PATH } = import.meta.env

export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getCart () {
      this.$http.get(`${VITE_APP_URL}/v2/api/${VIRE_APP_PATH}/cart`)
        .then((res) => {
          console.log(res)
          this.products = res.data.data.carts
        })
    }
  },
  mounted () {
    this.getCart()
  }
}
</script>
