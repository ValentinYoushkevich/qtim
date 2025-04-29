<template>
    <div class="flex items-center justify-center space-x-2 my-4">
        <button v-if="currentPage !== 1" class="px-4 py-2 border border-gray-300 bg-white rounded-lg"
            @click="goToPage(currentPage - 1)">
            <ChevronLeftIcon class="w-4 h-6 text-black" />
        </button>

        <button v-for="page in totalPages" :key="page" :class="[
            'px-3 py-1',
            page === currentPage
                ? 'bg-black text-white'
                : 'bg-gray-100 text-black',
        ]" class="px-4 py-2 rounded-lg" @click="goToPage(page)">
            {{ page }}
        </button>

        <button v-if="currentPage !== totalPages" class="px-4 py-2 border border-gray-300 bg-white rounded-lg"
            @click="goToPage(currentPage + 1)">
            <ChevronRightIcon class="w-4 h-6 text-black" />
        </button>
    </div>
</template>

<script setup>
import { ChevronLeftIcon, ChevronRightIcon } from '@heroicons/vue/24/solid';
import { computed, ref } from 'vue';
defineOptions({
    name: 'PostsPagination',
});
const emit = defineEmits(['update:currentPage']);
const props = defineProps({
    totalPosts: {
        type: Number,
        required: true
    },
    postsPerPage: {
        type: Number,
        default: 6
    }
});

const currentPage = ref(1);

const totalPages = computed(() => {
    return Math.ceil(props.totalPosts / props.postsPerPage);
});

const goToPage = (page) => {
    if (page < 1 || page > totalPages.value) return;
    currentPage.value = page;
    emit('update:currentPage', currentPage.value);
};
</script>

<style scoped></style>