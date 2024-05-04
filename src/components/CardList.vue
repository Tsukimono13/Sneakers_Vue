<script setup lang="ts">
import Card from './Card.vue';
interface Item {
    id: number;
    title: string;
    imageUrl: string;
    price: number;
}

defineProps<{ items: Item[] }>();

const onClickAdd = () => {
    console.log('add')
}
const onClickFavorite = () => {
    console.log('favorite')
}
</script>

<template>
    <div class="grid grid-cols-4 gap-5">
        <Card 
        v-for="item in items"
        :key="item.id"
        :title="item.title" 
        :img-url="item.imageUrl" 
        :price="item.price" 
        />
    </div>
</template>