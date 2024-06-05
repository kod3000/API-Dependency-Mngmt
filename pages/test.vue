<script setup lang="ts">

</script>

<template>
  <div class="image-grid p-2">
    <div class="image-row">
      <div class="image-item">
        <img src="/1.png" alt="Image 1" />
      </div>
      <div class="image-item">
        <img src="/2.png" alt="Image 2" />
      </div>
    </div>
    <div class="image-row">
      <div class="image-item">
        <img src="/3.png" alt="Image 3" />
      </div>
      <div class="image-item">
        <img src="/4.png" alt="Image 4" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.image-grid {
  display: flex;
  flex-direction: column;
  height: 60vh;
  width: 60vw;
}

.image-row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  height: 50%;
}

.image-item {
  flex-basis: 48%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-item img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
</style>
