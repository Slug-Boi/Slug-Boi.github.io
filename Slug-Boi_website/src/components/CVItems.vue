

<template>
    <v-timeline align="start">
        <v-timeline-item transition="slide-y-reverse-transition"
            v-for="(item, i) in items"
            :key="i"
            :dot-color="item.color"
            :icon="item.icon"
            fill-dot
            class="mx-auto"
            ref="timelineItems"
        >
            <v-card @click="item.show = !item.show" link>
                <v-card-title :class="['text-h6', `bg-${item.color}`]">
                    {{ item.title }}
                </v-card-title>
                <v-card-subtitle class="bg-purple-accent-4">
                    {{ item.position }}
                </v-card-subtitle>
                <v-expand-transition>
                    <div v-show="item.show">
                    <v-card-text class="text--primary bg-grey-darken-4">
                        <p>{{ item.description }}</p>
                    </v-card-text>
                </div>
                </v-expand-transition>
            </v-card>
        </v-timeline-item>
    </v-timeline>
</template>

<script setup lang="ts">

import { ref, onMounted, onBeforeUnmount } from 'vue';

const items = ref([
    {
        color: 'purple-darken-3',
        icon: 'mdi-star',
        title: "First item",
        description: "This is the first item",
        position: "Frontend Developer",
        inView: false,
        show: false,
        showDescription: false,
    },
    {
        color: 'purple-darken-3',
        icon: 'mdi-book-variant',
        title: "Second item",
        description: "This is the second item",
        position: "Backend Developer",
        inView: false,
        showDescription: false,
    },
    {
        color: 'purple-darken-3',
        icon: 'mdi-airballoon-outline',
        title: "Third item",
        description: "This is the third item",
        position: "Fullstack Developer",
        inView: false,
        showDescription: false,
    },
    {
        color: 'purple-darken-3',
        icon: 'mdi-layers-triple',
        title: "Fourth item",
        description: "This is the fourth item",
        position: "DevOps Engineer",
        inView: false,
        showDescription: false,
    },
]);

const timelineItems = ref([]);

</script>

<style>
.fade-in {
    opacity: 0;
    transition: opacity 1s ease-in;
}

.fade-in.in-view {
    opacity: 1;
}

</style>