<script setup lang="ts">
import CartHeader from './CartHeader.vue';
import CartList from './CartList.vue';
</script>
<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black bg-opacity-50 z-10"></div>
    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
        <CartHeader />
        <CartList />
        <div class="flex flex-col gap-3 mt-7">
            <div class="flex gap-2">
                <span>Итого:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>12990 руб.</b>
            </div>
            <div class="flex gap-2">
                <span>Налог 5%:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>549 руб.</b>
            </div>
            <button
                class="mt-4 bg-blue-400 w-full rounded-xl py-3 text-white disabled:bg-slate-300 cursor-pointer hover:bg-blue-500 active:bg-blue-600 transition">
                Оформить заказ
            </button>
        </div>
    </div>
</template>