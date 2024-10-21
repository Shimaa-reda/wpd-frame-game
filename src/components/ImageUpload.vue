<template>
  <div class="container nav mt-4">
    <img src="@/assets/images/logo.png" alt="Logo" class="logo" style="width:174px;" />
  </div>
  <div class="center-container">
    <div class="photo-container" @click="openFileInput">
      <input type="file" accept="image/*" ref="fileInput" @change="handlePhoto" style="display: none;" capture="user">

      <!-- In case no image is uploaded -->
      <div v-if="!imageUrl" class="icon-wrapper mb-5">
        <img src="@/assets/images/camera.png" alt="">
      </div>
      <p v-if="!imageUrl">
        <img src="@/assets/images/Capa 3.png" alt="" style="width:40px">
        Tap here to take a photo
      </p>

      <!-- In case an image is uploaded -->
      <div v-else class="image-wrapper">
        <img :src="imageUrl" class="uploaded-image" alt="Uploaded Image">
      </div>

      <!-- Button for retaking the photo -->
      <div v-if="imageUrl" class="retake-button-container">
        <button class="retake-button" @click="resetPhoto">
          <img src="@/assets/images/retake_camera.png" alt="Retake Icon" > Retake
        </button>
      </div>
    </div>
  </div>

  <div class="button-container" style="">
    <button class="back-button" v-if="imageUrl" @click="resetPhoto">Back</button>
    <button class="next-button" :disabled="!imageUrl" @click="goToNext">Next</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const imageUrl = ref(null);
const fileInput = ref(null);

const openFileInput = () => {
  fileInput.value.click(); // Open file input dialog
};

const handlePhoto = (event) => {
  const file = event.target.files[0];
  if (file) {
    // Create a URL for the uploaded image
    imageUrl.value = URL.createObjectURL(file);
    console.log("Photo captured:", file);
  }
};

const resetPhoto = () => {
  imageUrl.value = null; // Reset the image URL
};

const goToNext = () => {
  console.log("Next button clicked, proceed to the next step.");
};
</script>

<style>
body {
  background-image: url('@/assets/images/Rectangle.png');
  background-position: center; 
  background-repeat: no-repeat; 
  background-size: cover; 
  overflow-y: hidden;
   
  margin: 0; 
  display: flex; 
  flex-direction: column; 
}

.center-container {
  flex: 1;
  display: flex; 
  justify-content: center; 
  align-items: center; 
  flex-direction: column;
}

.button-container {
  position:relative;
  top: 80px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
}

.back-button {
  background-color: #7E3493;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 30px; 
  cursor: pointer;
  width: 150px;
  margin-bottom: 10px; 
}

.next-button {
  background-color: #7E3493;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 30px; 
  cursor: pointer;
  width: 150px;
  position: absolute;
  right: 20px;
  
}

.next-button:disabled {
  background-color: #808080; 
  cursor: not-allowed; 
}
.photo-container {
  width: 540px;
  height: 410px;
  border: 2px solid #FFFFFF;
  border-radius: 30px;
  background-color: #EAEAEA;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  text-align: center;
}

.icon-wrapper {
  margin-bottom: 10px;
}

.photo-container p {
  color: #888;
  font-size: 1.1rem;
}

.image-wrapper {
  display: flex;
  justify-content: center; 
  align-items: center; 
  height: 100%; 
}

.uploaded-image {
  max-width: 90%; 
  max-height: 70%; 
  object-fit: contain; 
  margin: 0; 
}

.retake-button-container {
  margin-top: 10px; 
  position: absolute; 
  bottom: 10px; 
}

.retake-button {
  background-color: white;
  border: 1px solid #A3A3A3;
  padding: 10px 20px;
  color: #7E3493;
  border-radius: 30px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center; 
  gap: 10px;
  width: 150px;
}



.retake-button img {
  width: 20px;
}
</style>
