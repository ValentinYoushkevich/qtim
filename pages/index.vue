<template>
    <div class="w-[1220px] mx-auto">
        <div v-if="posts" class="grid grid-cols-4 grid-rows-2 gap-2">
            <div v-for="post in posts" :key="post.id">
                <NuxtLink :to="`/posts/${post.id}`">
                    <div class="group relative bg-white p-2 max-w-[280px] h-[360px] flex flex-col">
                        <img class="w-full mt-auto" src="https://placehold.co/280x280" alt="Image">
                        <div class="pa-4">
                            <p class="text-gray-700 text-base line-clamp-3">
                                {{ post.description }}
                            </p>
                        </div>
                        <div class="hidden group-hover:block mt-2 text-blue-600 text-sm transition-all duration-300">
                            Read more
                        </div>
                    </div>
                </NuxtLink>
            </div>

        </div>
    </div>

</template>

<script setup lang="ts">
import type { Post } from '~/types/post'

defineOptions({
    name: 'PostsPage',
});

const { data: posts } = await useAsyncData<Post[]>(
    'posts',
    () => $fetch('https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/')
)

</script>

<style lang="scss" scoped></style>