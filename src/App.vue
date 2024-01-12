<script setup>
import { onMounted, provide, reactive, ref, watch } from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])

const drawerOpen = ref(false)

const filters = reactive({
    sortBy: 'name',
    searchQuery: ''
})

const onChangeSelect = (event) => {
    filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
    filters.searchQuery = event.target.value
}
const fetchFavorites = async () => {
    try {
        const { data: favorites } = await axios.get(`https://920ece1e14712716.mokky.dev/favorites`)
        items.value = items.value.map((item) => {
            const favorite = favorites.find((favorite) => favorite.parentId === item.id)

            if (!favorite) {
                return item
            }

            return {
                ...item,
                isFavorite: true,
                favoriteID: favorite.id
            }
        })
    } catch (error) {
        console.log(error)
    }
}

const addToFavorite = async (item) => {
    try {
        if (!item.isFavorite) {
            const obj = {
                parentId: item.id
            }
            item.isFavorite = true
            const { data } = await axios.post(`https://920ece1e14712716.mokky.dev/favorites`, obj)
            item.favoriteID = data.id
        } else {
            item.isFavorite = false
            await axios.delete(`https://920ece1e14712716.mokky.dev/favorites/${item.favoriteID}`)
            item.favoriteID = null
        }
    } catch (err) {
        console.log(err)
    }
}
const fetchItems = async () => {
    try {
        const params = {
            sortBy: filters.sortBy
        }

        if (filters.searchQuery) {
            params.name = `*${filters.searchQuery}*`
        }
        const { data } = await axios.get(`https://920ece1e14712716.mokky.dev/items`, {
            params
        })
        items.value = data.map((obj) => ({
            ...obj,
            isFavorite: false,
            favoriteID: null,
            isAdded: false
        }))
    } catch (error) {
        console.log(error)
    }
}

onMounted(async () => {
    await fetchItems()
    await fetchFavorites()
})
watch(filters, fetchItems)

provide('addToFavorite', addToFavorite)
</script>

<template>
    <Drawer v-if="drawerOpen" />
    <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
        <Header />
        <div class="p-10">
            <div class="flex justify-between items-center">
                <h2 class="text-3xl font-bold mb-8">All sneakers</h2>

                <div class="flex gap-4">
                    <select
                        @change="onChangeSelect"
                        class="py-2 px-3 border rounded-md outline-none"
                    >
                        <option value="name">By Name (A-Z)</option>
                        <option value="price">By Price (lower to higher)</option>
                        <option value="-price">By Price (higher to lower)</option>
                    </select>
                    <div class="relative">
                        <img src="/search.svg" alt="search" class="absolute left-4 top-3" />
                        <input
                            @input="onChangeSearchInput"
                            placeholder="Search..."
                            class="border rounded-md py-2 pr-4 pl-11 outline-none focus:border-gray-400"
                        />
                    </div>
                </div>
            </div>
            <div class="mt-10">
                <CardList :items="items" @addToFavorite="addToFavorite" />
            </div>
        </div>
    </div>
</template>

<style scoped></style>
