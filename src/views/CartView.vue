<script setup>
    import cartMethods from '../utils/cart';
    import { ref, watch } from 'vue';
    import { onMounted } from 'vue';

    const cart = ref([]);

    const fetchCart = () => {
        cart.value = cartMethods.getCart();
    }

    const removeItem = (id) => {
        cartMethods.removeFromCartById(id);
        cart.value = cartMethods.getCart();
    }

    const clearCart = () => {
        cartMethods.clearCart();
        cart.value = cartMethods.getCart();
    }

    onMounted(async () => {
        fetchCart();
    })
</script>

<template>
    <div>
        <h1 style="text-align: center; font-family: 'Times New Roman', Times, serif;">Carts</h1>
        <hr>
        <div v-for="item in cart" :key="item.id">
            <img :src="item.image" :alt="item.title" />
            <h3>{{ item.title }}</h3>
            <p>{{ item.price }}</p>
            <button @click="removeItem(item.id)">Remove</button>
        </div>

        <div v-if="cart.length === 0">
            <h3 style="text-align:center; font-family:'Times New Roman', Times, serif;">Cart is empty</h3>
        </div>

        <div v-if="cart.length > 0">
            <h3 style="text-align: center; font-family: 'Times New Roman', Times, serif;">Total: {{ cartMethods.getCartTotal() }} $</h3>
            <button @click="clearCart()">Clear cart</button>
        </div>
    </div>
</template>