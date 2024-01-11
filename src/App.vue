<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'

const items = ref([])
onMounted(async () => {
    // fetch('https://920ece1e14712716.mokky.dev/items')
    //     .then((res) => res.json())
    //     .then((data) => {
    //         console.log(data)
    //     })

    try {
        const { data } = await axios.get('https://920ece1e14712716.mokky.dev/items')
        items.value = data
    } catch (e) {
        console.log(e)
    }
})
</script>

<template>
    <!-- <Drawer /> -->
    <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
        <Header />
        <div class="p-10">
            <div class="flex justify-between items-center">
                <h2 class="text-3xl font-bold mb-8">All sneakers</h2>

                <div class="flex gap-4">
                    <select class="py-2 px-3 border rounded-md outline-none">
                        <option value="">By Name (A-Z)</option>
                        <option value="">By Price (cheaper)</option>
                        <option value="">By Price (higher)</option>
                    </select>
                    <div class="relative">
                        <img src="/search.svg" alt="search" class="absolute left-4 top-3" />
                        <input
                            placeholder="Search..."
                            class="border rounded-md py-2 pr-4 pl-11 outline-none focus:border-gray-400"
                        />
                    </div>
                </div>
            </div>
            <div class="mt-10">
                <CardList :items="items" />
            </div>
        </div>
    </div>
</template>

<style scoped></style>
