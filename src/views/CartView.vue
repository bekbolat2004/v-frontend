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
        <h1 style="text-align: center; font-family: 'Times New Roman', Times, serif;">Cart</h1>
        <hr>
        <div style="display:flex; flex-direction:row; margin: 30px;" v-for="item in cart" :key="item.id">
            <img style="width: 250px; height: 200px ;" :src="item.image" alt="item.title  " />
            <div style="font-family: 'Times New Roman', Times, serif; margin-left: 20px;" class="inf">
                <h2>Title:<strong>{{ item.title }}</strong></h2>
                <h3>Price:<strong>{{ item.price }}$</strong></h3>
                <button class="btn btn-primary" @click="removeItem(item.id)">Remove</button>
            </div>
        </div>

        <div style="text-align:center;" v-if="cart.length === 0">
            <h3 style="font-family:'Times New Roman', Times, serif;">Cart is empty</h3>
            <img src="https://www.eyecatchers.in/shop-online/images/cart-empty.jpg" alt="empty_cart">
        </div>

        <div style="margin: 30px;" v-if="cart.length > 0">
            <h3 style="font-family: 'Times New Roman', Times, serif;">Total sum: {{ cartMethods.getCartTotal() }} $</h3>
            <button class="btn btn-primary" @click="clearCart()">Clear cart</button>
        </div>
    </div>
</template>