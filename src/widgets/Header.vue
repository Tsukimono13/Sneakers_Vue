<template>
    <header class="flex justify-between border-b border-slate-200 px-10 py-8">
        <div class="flex items-center gap-4">
            <img src="/logo.png" alt="logo" class="w-10" />
            <div>
                <h1 class="text-xl font-bold uppercase">Vue Sneakers</h1>
                <p class="text-slate-400">Магазин лучших кроссовок</p>
            </div>
        </div>

        <ul class="flex items-center gap-10">
            <li class="flex items-center gap-3 cursor-pointer text-gray-600 hover:text-black">
                <img src="/cart.svg" alt="Card" />
                <b>1205 руб.</b>
            </li>
            <li class="flex items-center gap-3 cursor-pointer text-gray-600 hover:text-black">
                <img src="/heart.svg" alt="Card" />
                <span>Закладки</span>
            </li>
            <li class="flex items-center gap-3 cursor-pointer text-gray-600 hover:text-black">
                <img src="/profile.svg" alt="Card" />
                <span>Профиль</span>
            </li>
        </ul>
    </header>
</template>