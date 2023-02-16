<template>
  <div class="card">
  <img :src="product.imageUrl" class="card-img-top">
  <div class="card-body">
    <h2 class="card-title">{{ product.title }}</h2>
    <p class="card-text">{{ product.description }}</p>
    <p class="card-text">{{ product.content }}</p>
    <button type="button" class="btn btn-outline-primary" @click="addCart (product.id)">加入購物車</button>
  </div>
  </div>
</template>

<script>

const { VITE_APP_URL, VIRE_APP_PATH } = import.meta.env

export default {
  data () {
    return {
      product: {}
    }
  },
  methods: {
    getProduct () {
      const { id } = this.$route.params
      this.$http.get(`${VITE_APP_URL}/v2/api/${VIRE_APP_PATH}/product/${id}`)
        .then((res) => {
          console.log(res.data.product)
          this.product = res.data.product
        })
        .catch((err) => {
          console.log(err)
        })
    },
    addCart (id, qty = 1) {
      const data = {
        product_id: id,
        qty
      }
      this.$http.post(`${VITE_APP_URL}/v2/api/${VIRE_APP_PATH}/cart`, { data })
        .then((res) => {
          console.log(res)
        })
    }
  },
  mounted () {
    this.getProduct()
  }
}
</script>
