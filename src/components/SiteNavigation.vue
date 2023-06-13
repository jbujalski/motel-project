<template>
    <nav
        class="relative flex items-center flex-wrap justify-between p-4 lg:p-10 bg-white lg:bg-transparent lg:m-12 lg:absolute lg:top-0 lg:left-0 lg:right-0 lg:flex-row lg:flex-nowrap z-10">
        <div class="flex items-center flex-no-shrink text-white mr-6">
            <RouterLink :to="{ name: 'home' }">
                <div class="hidden lg:flex items-center gap-3 flex-1">
                    <img src="../assets/Logo-white.svg" class="h-12" />
                </div>
                <div class="flex lg:hidden items-center gap-3 flex-1">
                    <img src="../assets/Logo-black.svg" class="h-9" />
                </div>
            </RouterLink>
        </div>
        <div :class="!isOpen ? 'block' : 'hidden'" class="lg:hidden flex gap-4 flex-1 justify-end">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="h-10 cursor-pointer"
                @click="isOpen = !isOpen">
                <title>menu</title>
                <path d="M3,6H21V8H3V6M3,11H21V13H3V11M3,16H21V18H3V16Z" />
            </svg>
        </div>
        <div :class="isOpen ? 'block' : 'hidden'" class="lg:hidden flex gap-4 flex-1 justify-end">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="h-10 cursor-pointer"
                @click="isOpen = !isOpen">
                <title>close</title>
                <path
                    d="M19,6.41L17.59,5L12,10.59L6.41,5L5,6.41L10.59,12L5,17.59L6.41,19L12,13.41L17.59,19L19,17.59L13.41,12L19,6.41Z" />
            </svg>
        </div>
        <div :class="isOpen ? 'block' : 'hidden'"
            class="flex-col w-full static lg:flex lg:w-auto lg:flex-row z-10 gap-8 lg:text-white ">
            <RouterLink :to="{ name: 'home' }" activeClass="text-yellow-700 font-bold">
                <p class="p-3 hover:text-yellow-900 tracking-widest font-bold text-lg uppercase">
                    strona główna
                </p>
            </RouterLink>
            <RouterLink :to="{ name: 'rooms' }" activeClass="text-yellow-700">
                <p class="p-3 hover:text-yellow-900 tracking-widest font-bold text-lg uppercase">
                    pokoje
                </p>
            </RouterLink>
            <RouterLink :to="{ name: 'contact' }" activeClass="text-yellow-700">
                <p class="p-3 hover:text-yellow-900 tracking-widest font-bold text-lg uppercase">
                    kontakt
                </p>
            </RouterLink>
        </div>
    </nav>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";

const isOpen = ref(false);
</script>
