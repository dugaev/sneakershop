<script setup>
defineProps({
    imageURL: String,
    title: String,
    price: Number,
    isFavorite: Boolean,
    isAdded: Boolean,
    onClickAdd: Function,
    onClickFavorite: Function
})
</script>

<template>
    <div>
        <div
            class="relative border w-fit border-slate-100 rounded-3xl bg-white p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
        >
            <img
                :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
                alt="like"
                class="absolute top-8 left-8"
                @click="onClickFavorite"
            />
            <img :src="imageURL" alt="sneakers" />
            <p class="mt-2">
                {{ title }}
            </p>

            <div class="flex justify-between">
                <div class="flex flex-col">
                    <span class="text-slate-400">Price: </span>
                    <b>{{ price }}UAH</b>
                </div>
                <img
                    @click="onClickAdd"
                    :src="!isAdded ? '/plus.svg' : '/checked.svg'"
                    alt="plus"
                />
            </div>
        </div>
    </div>
</template>
