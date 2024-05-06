<script setup lang="ts">
import { onMounted, provide, reactive, ref, watch } from 'vue';
import Header from './widgets/Header.vue';
import CardList from './components/CardList.vue';
import Drawer from './components/Drawer.vue';
import axios from 'axios';

interface EventType extends Event {
  target: HTMLInputElement;
}

interface ItemType {
  id: number,
  title: string,
  price: number,
  imageUrl: string
}

interface FavoriteType extends ItemType {
  parentId: number;
}

const items = ref<ItemType[]>([]);
const drawerOpen = ref(false);

const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const filters = reactive({
  sortBy: "title",
  searchQuery: "",
});

const onChangeSelect = (event: EventType) => {
  filters.sortBy = event.target.value;
}

const onChangeSearchInput = (event: EventType) => {
  filters.searchQuery = event.target.value
}

const addToFavorite = async (item: any) => {
  try {
   if (!item.isFavorite) {
    const obj = {
      parentId: item.id
    }

    item.isFavorite = true

    const { data } = await axios.post<any>(`https://c73785999a69886f.mokky.dev/favorites`, obj);

    item.favoriteId = data.id
   } else {
    item.isFavorite = false
    await axios.delete(`https://c73785999a69886f.mokky.dev/favorites/${item.favoriteId}`);
    item.favoriteId = null
   }
  } catch (error) {
    console.log(error)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get<FavoriteType[]>(`https://c73785999a69886f.mokky.dev/favorites`);
    items.value = items.value.map((item: any) => {
      const favorite = favorites.find(favorite => favorite.parentId === item.id)

      if (!favorite) {
        return item
      }

      return { ...item, isFavorite: true, favoriteId: favorite.id };
    })
  } catch (error) {
    console.log(error)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }
    const { data } = await axios.get(`https://c73785999a69886f.mokky.dev/items`, {
      params
    })
    items.value = data.map((item: ItemType) => ({ 
      ...item, 
      isFavorite: false, 
      favoriteId: null,
      isAdded: false
     }));
  } catch (error) {
    console.log(error)
  }
}

onMounted(async () => {
  await fetchItems();
  await fetchFavorites()
});
watch(filters, fetchItems);

provide('cartActions', {
  closeDrawer,
  openDrawer
})
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
    <Header @open-drawer="openDrawer"/>
    <Drawer v-if="drawerOpen" />
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
            <input @input="onChangeSearchInput"
              class="border border-slate-200 py-2 pl-10 pr-4 rounded-md outline-none focus:border-gray-400"
              placeholder="Поиск..." type="text" />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" @add-to-favorite="addToFavorite" />
      </div>

    </div>
  </div>
</template>

<style scoped></style>
