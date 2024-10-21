<template>
  <div>
    <h3>Select a Frame</h3>
    <div class="frames">
      <div
        v-for="frame in frames"
        :key="frame.id"
        :style="{ backgroundImage: `url(${frame.src})` }"
        class="frame"
        @click="selectFrame(frame.src)"
      ></div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const frames = ref([
  { id: 1, src: 'path/to/frame1.png' },
  { id: 2, src: 'path/to/frame2.png' },
  { id: 3, src: 'path/to/frame3.png' },
]);

const selectedFrame = ref(null);

const selectFrame = (src) => {
  selectedFrame.value = src;
};
</script>

<style scoped>
.frames {
  display: flex;
  gap: 10px;
}
.frame {
  width: 100px;
  height: 100px;
  border: 2px solid #ccc;
  background-size: cover;
  cursor: pointer;
}
.frame:hover {
  border-color: #000;
}
</style>
