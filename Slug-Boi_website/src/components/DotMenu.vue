<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const sections = ref([
    { id: 'section1', name: 'Section 1' },
    { id: 'section2', name: 'Section 2' },
    { id: 'section3', name: 'Section 3' },
    { id: 'section4', name: 'Section 4' }
]);

const isVisible = ref(false);
const selectedSection = ref<string | null>(null);

function scrollToSection(id: string) {
    const element = document.getElementById(id);
    if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
        selectedSection.value = id;
    }
}

function highlightSection(id: string) {
    const element = document.getElementById(id);
    if (element) {
        element.classList.add('highlight');
    }
}

function removeHighlight(id: string) {
    const element = document.getElementById(id);
    if (element) {
        element.classList.remove('highlight');
    }
}

function handleScroll() {
    const scrollPosition = window.scrollY;
    if (scrollPosition > 140) { // Adjust this value as needed
        isVisible.value = true;
    } else {
        isVisible.value = false;
    }
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll);

    onUnmounted(() => {
        window.removeEventListener('scroll', handleScroll);
    });
});
</script>

<template>
    <div :class="['dot-menu', { 'fade-in': isVisible }]">
        <div 
            v-for="(section, index) in sections" 
            :key="index" 
            :class="['dot-container', { 'selected': selectedSection === section.id }]"
            @click="scrollToSection(section.id)"
            @mouseover="highlightSection(section.id); selectedSection = section.id"
            @mouseleave="removeHighlight(section.id); selectedSection = null"
        >
            <span class="section-name" v-if="selectedSection === section.id">{{ section.name }}</span>
            <div :class="['dot', { 'selected': selectedSection === section.id }]"></div>
        </div>
    </div>
</template>

<style scoped>
.dot-menu {
    position: fixed;
    top: 50%;
    right: 20px;
    transform: translateY(-50%);
    display: flex;
    flex-direction: column;
    gap: 10px;
    opacity: 0;
    transition: opacity 0.5s;
    z-index: 1000;
}

.dot-menu.fade-in {
    opacity: 1;
}

.dot-container {
    position: relative; /* Add relative positioning */
    display: flex;
    align-items: center;
    gap: 10px;
    width: 50px; /* Set a fixed width for the container */
}

.section-name {
    position: absolute; /* Use absolute positioning */
    left: 30px; /* Adjust the position as needed */
    font-size: 14px;
    color: white; /* TODO: Change to a nice cyber pink */
    white-space: nowrap;
    transform: translateX(-140%);
    pointer-events: none; /* Ensure the text does not interfere with hover events */
    opacity: 0; /* Start with the text hidden */
    transition: opacity 0.5s; /* Add a transition for the opacity */
}

.dot-container.selected .section-name {
    opacity: 1; /* Show the text when the dot is selected */
}

.dot {
    width: 8px;
    height: 8px;
    background-color: gray;
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s, width 0.3s;
    margin: 0 auto; /* Center the dot within the container */
}

.dot:hover {
    background-color: black;
}

.dot.selected {
    width: 25px;
    border-radius: 5px;
}

.highlight {
    background-color: yellow;
}
</style>
