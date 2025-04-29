<template>
    <div class="w-[1220px] mx-auto">
        <div v-if="currentPosts">
            <h1 class="text-7xl leading-none mb-12">Articles</h1>
            <div class="grid grid-cols-4 grid-rows-2 gap-2">
                <div v-for="post in currentPosts" :key="post.id">
                    <NuxtLink :to="`/posts/${post.id}`">
                        <div class="group relative bg-white p-2 max-w-[280px] h-[360px] flex flex-col">
                            <div class="absolute bottom-[50%] right-5">{{ post.id }}</div>
                            <!-- <img class="w-full mt-auto rounded-lg" :src=post.image alt="Image"> -->
                            <img class="w-full mt-auto rounded-lg" src="https://placehold.co/280x280" alt="Image">
                            <div class="pa-4">
                                <p class="text-gray-700 text-base line-clamp-3">
                                    {{ post.description }}
                                </p>
                            </div>
                            <div
                                class="hidden group-hover:block mt-2 text-blue-600 text-sm transition-all duration-300">
                                Read more
                            </div>
                        </div>
                    </NuxtLink>
                </div>
            </div>
            <PostsPagination v-if="currentPosts.length > 0" v-model="currentPage"
                :total-posts="allPosts ? allPosts.length : 0" @update:current-page="goToPage"
                :postsPerPage="postsPerPage" />
        </div>
        <div v-else class="w-[1220px] mx-auto"> No data about posts</div>
    </div>
</template>

<script setup lang="ts">
import type { Post } from '~/types/post';

defineOptions({
    name: 'PostsPage',
});

const currentPosts = ref<Post[]>([]);

const currentPage = ref(1);

const postsPerPage = 8;

const { data: allPosts } = await useAsyncData<Post[]>(
    'posts',
    () => $fetch('https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/')
)
const updateCurrentPosts = () => {
    const start = (currentPage.value - 1) * postsPerPage;
    const end = start + postsPerPage;
    if (allPosts && allPosts.value) {
        currentPosts.value = allPosts.value.slice(start, end);
    }
};

const goToPage = (page: number) => {
    if (page < 1) return;
    currentPage.value = page;
    updateCurrentPosts();
};

watch(currentPage, updateCurrentPosts);

onMounted(updateCurrentPosts);
</script>

<style lang="scss" scoped></style>