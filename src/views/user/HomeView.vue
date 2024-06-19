<script setup>
import { useRouter } from 'vue-router'
import UserLayout from '@/layouts/UserLayout.vue'
import Product from '@/components/Product.vue'

import { useUserProductStore } from '@/stores/user/product.js'
import { useCartStore } from '@/stores/user/cart.js'

const router = useRouter()

const productStore = useUserProductStore()
const cartStore = useCartStore()

const addToCart = (product) => {
    cartStore.addToCart(product)
    router.push({ name: 'cart' })
}
</script>

<template>
    <UserLayout>
        <!-- Hero -->
        <div class="hero h-96 bg-base-200">
            <div class="hero-content text-center">
                <div class="max-w-md">
                    <h1 class="text-5xl font-bold">Hello to My Shop</h1>
                    <p class="py-6">Create by Github : Morninguoou</p>
                </div>
            </div>
        </div>
        <Product 
            :products="productStore.list"
            :addToCart="addToCart">
        </Product>
    </UserLayout>
</template>