<template>
  <main>
    <figure class=" mb-6">
      <Transition
        appear
        mode="out-in"
        enter-from-class="opacity-0 -translate-y-2"
        leave-to-class="opacity-0 -translate-y-2"
        enter-active-class="transition duration-100"
        leave-active-class="transition duration-100"
      >
        <img
          :key="state.id"
          class="rounded-3xl h-80 shadow-xl overflow-hidden w-52  object-cover"
          :src="state.url"
          :alt="'img' + state.id"
        >
      </Transition>
    </figure>
    <div class="relative">
      <button type="button" class="right-full absolute top-6 -rotate-12" @click="prev()" @keyup.left="prev()">
        <i class='bx bx-md bxs-left-arrow'></i>
      </button>
      <button type="button" class="left-full absolute top-6 rotate-12" @click="next()" @keyup.right="next()">
        <i class='bx bx-md bxs-right-arrow'></i>
      </button>
      <ul class="flex justify-evenly">
        <li v-for="({ id, url }, index) in previewImg" :key="id" @click="go(index)"
          class="cursor-pointer first:-rotate-12 first:translate-y-2 last:rotate-12 last:translate-y-2">
          <img class="shadow-lg rounded-2xl w-11 h-11" :src="url" :alt="'img' + id">
        </li>
      </ul>
    </div>
    <p class="font-bold text-center leading-loose">{{ index + 1 }} / {{ list.length }}</p>
  </main>
</template>

<script setup>
import { computed } from 'vue'
import { useCycleList } from '@vueuse/core'

const list = [
  {
    id: 0,
    url: './img/img-1.jpg'
  },
  {
    id: 1,
    url: './img/img-2.jpg',
  },
  {
    id: 2,
    url: './img/img-3.jpg'
  },
  {
    id: 3,
    url: './img/img-4.jpg'
  },
  {
    id: 4,
    url: './img/img-5.jpg'
  },
  {
    id: 5,
    url: './img/img-6.jpg'
  },
  {
    id: 6,
    url: './img/img-7.jpg'
  },
  {
    id: 7,
    url: './img/img-8.jpg'
  },
  {
    id: 8,
    url: './img/img-9.jpg'
  },
  {
    id: 9,
    url: './img/img-10.jpg'
  },
  {
    id: 10,
    url: './img/img-11.jpg'
  }
]

const go = index => {
  if (index < 1) {
    prev()
  } else if (index > 1) {
    next()
  }
}

const previewImg = computed(() => {
  const initIndex = [index.value - 1, index.value, index.value + 1]
  const validIndex = initIndex.map(item => {
    if (item < 0) {
      return list.length - 1
    } else if (item >= list.length) {
      return 0
    } else {
      return item
    }
  })
  return validIndex.map(itemIndex => {
    return list.find((img, index) => index === itemIndex)
  })
})

const { state, next, prev, index } = useCycleList(list)
</script>