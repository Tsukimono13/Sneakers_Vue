<script lang="ts" setup>
defineProps({
    imgUrl: String,
    title: String,
    price: Number,
    isAdded: Boolean,
    isFavorite: Boolean,
    onClickAdd: Function,
    onClickFavorite: Function
})
</script>

<template>
    <div
        class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
        <img 
        @click="onClickFavorite"
        :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" 
        alt="Like" 
        class="absolute top-8 left-8" />
        <img :src="imgUrl" alt="Sneakers" />
        <p class="mt-2">{{ title }}</p>
        <div class="flex justify-between mt-5">
            <div>
                <p class="text-slate-400">Цена:</p>
                <b>{{ price }} руб.</b>
            </div>
            <img @click="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Add" />
        </div>
    </div>
</template>