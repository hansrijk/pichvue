<script setup>
import { ref, nextTick } from 'vue';

const isVisible = ref(true);
var maxRandomRespawnTime = 3;

function handleClick() {
  isVisible.value = !isVisible.value;

  // wait a random amount of seconds and make it re-appear
  var randomRespawnTime = Math.floor(Math.random() * maxRandomRespawnTime);
  console.log("Pichu will re-appear in: " + randomRespawnTime + " seconds...");
  setTimeout(async () => {
    isVisible.value = true;
    
    // wait for DOM to update
    await nextTick();
    
    // appear at a random location
    const img = document.querySelector('.pichu-image');
    const imgWidth = 300 * (img.naturalWidth / img.naturalHeight); // calculate width based on aspect ratio
    const imgHeight = 300;
    
    const x = Math.random() * (window.innerWidth - imgWidth);
    const y = Math.random() * (window.innerHeight - imgHeight);
    
    img.style.left = `${x}px`;
    img.style.top = `${y}px`;

  }, randomRespawnTime * 1000);
}
</script>

<template>

<div style="position: relative; height: 100vh; overflow: hidden;">
    <img
      v-if="isVisible"
     src="/Pichu.png"
      alt="Pichu"
      @click="handleClick"
      class="pichu-image" 
      style="position: absolute;"
      height="300px">
</div>
</template>

<style>
html, body, #app {
  height: 100%;
}
body {
  margin: 0;
  background-color: gray;
}
</style>
