<script setup>
  import {useRoute} from "vue-router";
  import axios from "axios";
  import {onMounted, ref} from "vue";

  const route = useRoute()
  const isLoaded = ref(false)
  const product = ref({})
  const fetchProduct = async () => {
      isLoaded.value = false
      const product_req = await axios.get(`http://localhost:8000/api/products/${route.params.id}`)
      product.value = product_req.data
      isLoaded.value = true
  }
  onMounted(async () => {
      await fetchProduct()
  })
</script>

<template>
<div class="container-sm sticky-sm-top" style="width: 17%; position: static; "><img :src="product.image" class="card-img-top" :alt="product.title">
</div>
    <div class="card-body" style="text-align: center; margin-left:200px; margin-right: 200px; font-family: 'Times New Roman', Times, serif;">
        <h2 class="card-title">Title:{{product.title }}</h2>
        <h3 class="card-text">Price:{{ product.price }}$</h3>
        <h4>Description: {{ product.description }}</h4>
    </div>
<!--
<div>
      <h1>Product</h1>
      <div v-if="isLoaded">
      <p>{{ product.title }}</p>
      </div>
      <div v-else>
          ...loading
      </div>
  </div>
-->
</template>