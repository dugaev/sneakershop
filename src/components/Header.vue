<template>
    <header class="flex justify-between border-b border-slate-200 py-8 px-10">
        <div class="flex items-center gap-4">
            <img src="/favicon.svg" alt="Logo" class="w-[90px] h-[70px]" />
            <div>
                <h2 class="text-xl font-bold uppercase">SneakerShop</h2>
                <p class="text-slate-500">Buy your favorite sneakers</p>
            </div>
        </div>

        <ul class="flex items-center gap-10">
            <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
                <img src="/cart.svg" alt="cart" />
                <b>1200 UAH</b>
            </li>
            <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
                <img src="/heart.svg" alt="heart" />
                <span>Favorite</span>
            </li>
            <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
                <img src="/profile.svg" alt="profile" />
                <span>Profile</span>
            </li>
        </ul>
    </header>
</template>
