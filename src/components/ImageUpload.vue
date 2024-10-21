<template>
  <!-- <div>
    <input type="file" @change="onFileChange" accept="image/*" />
    <img v-if="imageUrl" :src="imageUrl" alt="Uploaded Image" class="uploaded-image" />
  </div> -->
  <div class="container">
    
  </div>
</template>

<script setup>
import { ref } from 'vue';

const imageUrl = ref(null);

const onFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    imageUrl.value = URL.createObjectURL(file);
  }
};
</script>

<style >
.uploaded-image {
  max-width: 300px;
  margin-top: 10px;
}
body {
  background-image: url('@/assets/images/Rectangle.png');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover; /* Resize the background image to cover the entire container */
}

</style>
