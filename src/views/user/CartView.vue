<script setup>
import { RouterLink } from 'vue-router'

import UserLayout from '@/layouts/UserLayout.vue'
import CloseIcon from '@/components/icons/Close.vue'

import { useCartStore } from '@/stores/user/cart';

const cartStore = useCartStore()

console.log(cartStore.items)

const changeQuantity = (event, index) => {
    const newQuantity = parseInt(event.target.value)
    cartStore.updateQuantity(index, newQuantity)
}

</script>

<template>
    <UserLayout>
        <h1 class="text-3xl font-bold m-4">Shopping Cart</h1>
        <div class="flex">
            <div class="flex-auto w-64 bg-base-200 p-4">
                <div v-if="cartStore.items.length === 0">
                    Cart is empty
                </div>
                <div v-else v-for="(item, index) in cartStore.items" class="flex">
                    <div class="flex-1">
                        <img class="w-full p-10" :src="item.imageUrl">
                    </div>
                    <div class="flex-1">
                        <div class="flex flex-col justify-between h-full">
                            <div>
                                <div class="relative grid grid-cols-2">
                                    <div>
                                        <div><b>{{item.name}}</b></div>
                                        <div>{{item.about}}</div>
                                        <div>{{item.price}} B</div>
                                    </div>
                                    <div>
                                        <select v-model="item.quantity" @change="changeQuantity($event, index)" class="select mx-8 w-2/3"> 
                                            <option v-for="quantity in [1,2,3,4,5]">
                                                {{ quantity }}
                                            </option>
                                        </select>
                                    </div>
                                    <div @click="cartStore.removeItemInCart(index)" class="absolute top-3 right-0">
                                        <CloseIcon></CloseIcon>
                                    </div>
                                </div>
                            </div>
                            <div><b>{{item.status}}</b></div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="flex-auto w-32 bg-slate-200 p-4">
                <div class="text-xl font-bold">Order Summary</div>
                <div class="my-4 divide-y divide-black">
                    <div class="flex justify-between p-2">
                        <div>ราคาสินค้าทั้งหมด</div>
                        <div>{{ cartStore.summaryPrice }}</div>
                    </div>
                    <div class="flex justify-between p-2">
                        <div>ค่าส่ง</div>
                        <div>0</div>
                    </div>
                    <div class="flex justify-between p-2">
                        <div>ราคารวมทั้งหมด</div>
                        <div>{{ cartStore.summaryPrice }}</div>
                    </div>
                    <RouterLink :to="{ name: 'checkout' }" class="btn btn-neutral w-full mt-4">
                        ชำระเงิน
                    </RouterLink>
                </div>
            </div>
        </div>
    </UserLayout>
</template>