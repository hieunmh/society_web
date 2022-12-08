<template>
    <guest-layout>
        <section class="flex md:flex-row m-2 p-2">
            <div class="w-8/12">
                <PostCard v-for="post in posts.data" :post="post" :community="post.community_slug" :key="post.id" />
            </div>

            <div class="w-4/12 p-4">
                <CommunityList :communities="communities">
                    <template #title>Top Communities</template>
                </CommunityList>
            </div>
        </section>
    </guest-layout>

</template>

<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import PostCard from '@/Components/PostCard.vue';
import Pagination from '@/Components/Pagination.vue';
import CommunityList from '@/Components/CommunityList.vue';
import { ref, watch } from 'vue';
import { Inertia } from '@inertiajs/inertia';

const props = defineProps({
    communities: Object,
    posts: Object,
})

const search = ref('');
watch(search, value => {
    Inertia.get('/', {search: value});
});
</script>