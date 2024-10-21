<template>
  <div class="preview-container">
    <div v-if="imageUrl && selectedFrame" class="frame-preview">
      <img :src="selectedFrame" class="frame-image" />
      <img :src="imageUrl" class="uploaded-image" />
    </div>
    <div v-else>
      <p>Please upload an image and select a frame.</p>
    </div>
  </div>
</template>

<script setup>
import { toRefs } from 'vue';

const props = defineProps(['imageUrl', 'selectedFrame']);
</script>

<style scoped>
.preview-container {
  position: relative;
}

.frame-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
}

.uploaded-image {
  width: 100%;
}
</style>
