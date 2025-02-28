<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue';
import video from '../assets/Slug_animation_fixed.mp4';

const handleScroll = () => {
  const videoElement = document.querySelector('.LoopedVideo') as HTMLVideoElement;
  const scrollPosition = window.scrollY;
  videoElement.style.transform = `translateY(${scrollPosition * 0.5}px)`;
};

const scrollToContent = () => {
  window.scrollBy({ top: 500, behavior: 'smooth' });
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <div class="ParallaxVideo">
    <video class="LoopedVideo" autoplay loop muted>
      <source :src="video" type="video/mp4">
    </video>
    <button @click="scrollToContent" class="scroll-button">Scroll Down</button>
  </div>
</template>

<style scoped>
@keyframes jump {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.ParallaxVideo {
  position: relative;
  width: 100%;
  height: 500px;
  overflow: hidden;
  background-color: black;
  z-index: 0;
}

.LoopedVideo {
  position: absolute;
  top: -70%;
  left: -16%;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
  z-index: 1;
  will-change: transform;
}

.scroll-button {
  position: absolute;
  bottom: 20px;
  left: 47%;
  padding: 10px 20px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  z-index: 2;
  transition: transform 0.3s;
}

.scroll-button:hover {
  animation: jump 0.6s infinite;
}
</style>