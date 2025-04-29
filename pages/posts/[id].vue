<template>
    <div v-if="post" class="w-[1220px] mx-auto">
        <h1 class="text-3xl font-bold mb-4 mt-[80px]">{{ post.title }}</h1>
        <img class="w-full mt-auto object-cover" src="https://placehold.co/1200x700" alt="Image">
        <div class="mt-8 text-black-600 text-base text-[16px] leading-[20px]">About</div>
        <p class="w-1/2 text-black-600 text-base text-[24px] leading-[36px] mt-2">
            {{ post.description }}
        </p>
    </div>
    <div v-else class="w-[1220px] mx-auto"> No data about post</div>
</template>

<script setup lang="ts">
import type { Post } from '~/types/post'

const route = useRoute();
const id = route.params.id;
const { data: post } = await useAsyncData<Post>(
    'post',
    () => $fetch(`https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/${id}`)
)

</script>