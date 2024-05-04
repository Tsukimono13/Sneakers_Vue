<script setup lang="ts">
import { onMounted, ref, watch } from 'vue';
import Header from './widgets/Header.vue';
import CardList from './components/CardList.vue';
import Drawer from './components/Drawer.vue';
import axios from 'axios';

const items = ref([]);
const sortBy = ref('');
const searchQuery = ref('');

const onChangeSelect = (event: Event) => {
  const select = event.target as HTMLSelectElement | '';
  if (select) {
    sortBy.value = select.value;
  }
}

onMounted(async () => {
  try {
    const {data} = await axios.get('https://c73785999a69886f.mokky.dev/items')
    items.value = data;
  } catch (error) {
    console.log(error)
  }
});

watch(sortBy, async() => {
  try {
    const {data} = await axios.get('https://c73785999a69886f.mokky.dev/items?sortBy=' + sortBy.value)
    items.value = data;
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
    <Header />
    <!-- <Drawer /> -->
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
        <select @change="onChangeSelect" class="py-2 border rounded-md outline-none">
          <option value="name">По названию</option>
          <option value="price">По возрастанию</option>
          <option value="-price">По убыванию</option>
        </select>

        <div class="relative">
          <img class="absolute top-3.5 left-3" src="/search.svg" alt="Search" />
          <input class="border border-slate-200 py-2 pl-10 pr-4 rounded-md outline-none focus:border-gray-400"
            placeholder="Поиск..." type="text" />
        </div>
      </div>
    </div>

    <div class="mt-10">
      <CardList :items="items"/>
    </div>

    </div>
  </div>
</template>

<style scoped></style>
