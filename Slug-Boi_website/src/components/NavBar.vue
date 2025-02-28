<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue';

const imageExists = ref(true);
const scrollY = ref(0);

const handleScroll = () => {
  scrollY.value = window.scrollY*2;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});

const navbarOpacity = computed(() => {
  return scrollY.value > 50 ? 0 : 1;
});
</script>

<template>
  <nav :style="{ opacity: navbarOpacity, transition: 'opacity 0.5s' }">
    <ul>
      <li>
        <a href="#home" class="disable_hover">
          <img v-if="imageExists" src="../assets/logo.png" alt="Logo" style="width: 50px; height: 50px;">
        </a>
      </li>
      <li><a href="#home">Home</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#blog">Blog</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</template>

<style scoped>
nav {
  background-color: transparent;
  overflow: hidden;
  position: absolute;
  z-index: 2;
}

.disable_hover :hover {
  background-color: transparent;
}

nav ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

nav ul li {
  float: left;
}

nav ul li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

nav ul li a:hover {
  background-color: #111;
}
</style>
