<script setup>
import { ref, onMounted } from 'vue';

import { useCartStore } from '@/stores/user/cart'

import UserLayout from '@/layouts/UserLayout.vue'

const cartStore = useCartStore()
const orderData = ref({})

onMounted(() =>{
    cartStore.loadCheckout()
    if (cartStore.checkout.orderNumber){
        orderData.value = cartStore.checkout
    }
})
</script>

<template>
    <UserLayout>
        <div class="max-w-3xl mx-auto my-8 border border-base-200 shadow-xl">
            <div class="m-5">
            <div>
                <div class="text-3xl font-semibold">Your order is successful</div>
                <div>Hi,{{orderData.name}}</div>
                <div>เครียมรอรับสินค้าของคุณได้เลย</div>
            </div>
            <div class="divider"></div>
            <div class="grid grid-cols-4 gap-2">
                <div>
                    <div class="font-bold">Order date</div>
                    <div class="font-medium">{{orderData.createdDate}}</div>
                </div>
                <div class="ml-4">
                    <div class="font-bold">Order Number</div>
                    <div class="font-medium">{{orderData.orderNumber}}</div>
                </div>
                <div>
                    <div class="font-bold">Payment method</div>
                    <div class="font-medium">{{orderData.paymentMethod}}</div>
                </div>
                <div class="ml-4">
                    <div class="font-bold">Address</div>
                    <div class="font-medium">{{orderData.address}}</div>
                </div>
            </div>
            <div class="divider"></div>
            <div v-for="product in orderData.products" class="grid grid-cols-4 gap-2 mb-4 items-center">
                <div>
                    <img class="w-full" :src="product.imageUrl">
                </div>
                <div class="ml-4">
                    <b>{{ product.name }}</b>
                </div>
                <div>
                    จำนวน : {{ product.quantity }}
                </div>
                <div class="ml-4">
                    ราคารวม {{ product.price * product.quantity }}
                </div>
            </div>
            <div class="divider"></div>
            <div class="flex justify-between">
                <div class="font-bold">ราคาสินค้าทั้งหมด</div>
                <div class="font-medium">{{orderData.totalPrice}}</div>
            </div>
            <div class="flex justify-between">
                <div class="font-bold">ค่าส่ง</div>
                <div class="font-medium">0</div>
            </div>
            <div class="divider"></div>
            <div class="flex justify-between">
                <div class="font-bold">ราคาทั้งสิ้น</div>
                <div class="font-medium">{{orderData.totalPrice}}</div>
            </div>
            <div class="divider"></div>
            <div>ขอบคุณที่มาซื้อสินค้าของเรา</div>
        </div>
        </div>
    </UserLayout>
</template>