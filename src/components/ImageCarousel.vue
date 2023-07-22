<script setup>


import { ref, reactive } from 'vue'
const images = reactive([
    {
        id: 1,
        ImageSmallUrl: '/img/picture1.jpeg',
        imageLargeUrl: '/img/picture1_large.jpeg',
        title: 'Kitchen Workstation',
        subtitle: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.'
    },
    {
        id: 2,
        ImageSmallUrl: '/img/picture2.jpeg',
        imageLargeUrl: '/img/picture2_large.jpeg',
        title: 'MakeUp Station',
        subtitle: 'aliquam molestiae consectetur dolor, temporibus reprehenderit! '
    },
    {
        id: 3,
        ImageSmallUrl: '/img/picture3.jpeg',
        imageLargeUrl: '/img/picture3_large.jpeg',
        title: 'TV cabinet',
        subtitle: 'ipsam minus porro temporibus eos provident nisi quod molestias!'
    },
    {
        id: 4,
        ImageSmallUrl: '/img/picture4.jpeg',
        imageLargeUrl: '/img/picture4_large.jpeg',
        title: 'Washing place',
        subtitle: 'dolorum quibusdam magni voluptatibus aperiam neque odit!'
    }
])

const currentSlide = ref(0)

const nextSlide = () => {
    currentSlide.value++
    if (currentSlide.value >= images.length)
        currentSlide.value = 0
}

const prevSlide = () => {
    if (currentSlide.value == 0)
        currentSlide.value = images.length - 1
    else
        currentSlide.value--
}

let timerPause = 0
const timerFunc = () => {
    timerPause = 0
    setTimeout(() => {
        if (!timerPause)
            nextSlide()
        timerFunc()
    }, 5000)
}

timerFunc()

</script>

<template>
    <div class="relative m-5 bg-gray-50">
        <!-- image -->
        <div class="flex justify-center items-center relative overflow-hidden rounded-lg p-2 ">
            <img class="h-[75vh] mb-10" :src="images[currentSlide].ImageSmallUrl">
        </div>
        <div class="absolute inset-x-[15%] bottom-12 py-5 text-center text-white md:block">
            <h5 class="text-xl">{{ images[currentSlide].title }}</h5>
            <p class="text-sm truncate  text-center">{{ images[currentSlide].subtitle }}
            </p>
        </div>
        <!-- Slider indicators -->
        <div class="absolute z-30 flex space-x-3  -translate-x-1/2 bottom-5 left-1/2">
            <button v-for="iml in images.length" :key="iml" id="carousel-indicator-1" type="button"
                class="w-3 h-3 rounded-full border-white" :class="currentSlide == (iml - 1) ? 'bg-red-700' : 'bg-gray-600'"
                @click="timerPause = 1; currentSlide = (iml - 1)"></button>
        </div>

        <!-- Slider controls -->
        <button @click="prevSlide" id="data-carousel-prev" type="button"
            class="absolute top-0 left-0 z-30 flex items-center justify-center h-full px-4 cursor-pointer group focus:outline-none">
            <span
                class="inline-flex items-center justify-center w-10 h-10 rounded-full bg-orange/30 dark:bg-gray-800/30 group-hover:bg-orange/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
                <svg class="w-4 h-4 text-orange-600 dark:text-gray-800" aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 6 10">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M5 1 1 5l4 4" />
                </svg>
                <span class="hidden">Previous</span>
            </span>
        </button>

        <button @click="nextSlide" id="data-carousel-next" type="button"
            class="absolute top-0 right-0 z-30 flex items-center justify-center h-full px-4 cursor-pointer group focus:outline-none">
            <span
                class="inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/30 dark:bg-gray-800/30 group-hover:bg-orange/50 dark:group-hover:bg-gray-800/60 group-focus:ring-4 group-focus:ring-white dark:group-focus:ring-gray-800/70 group-focus:outline-none">
                <svg class="w-4 h-4 text-orange-600 dark:text-gray-800" aria-hidden="true"
                    xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 6 10">
                    <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="m1 9 4-4-4-4" />
                </svg>
                <span class="hidden">Next</span>
            </span>
        </button>
    </div>
</template>

<style scoped>
</style>
