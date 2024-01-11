<script setup>
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'
</script>

<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black/70 z-10"></div>
    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
        <DrawerHead />
        <CartItemList />

        <div class="flex flex-col gap-4 mt-7">
            <div class="flex gap-2">
                <span>Overall: </span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>12900 UAH</b>
            </div>
            <div class="flex gap-2">
                <span>Discount: </span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>5%</b>
            </div>
            <button
                disabled=""
                class="mt-2 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-400 disabled:cursor-not-allowed"
            >
                Order Now!
            </button>
        </div>
    </div>
</template>
