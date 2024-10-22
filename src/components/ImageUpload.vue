<template>
  <div class="container nav">
    <img
      src="@/assets/images/logo.png"
      alt="Logo"
      class="logo"
      style="width: 174px"
    />
  </div>
  <div class="center-container">
    <div class="photo-frame-container">
      <div class="photo-container" @click="openFileInput">
        <div class="content" >
          <input
            type="file"
            accept="image/*"
            ref="fileInput"
            @change="handlePhoto"
            style="display: none"
            capture="user"
          />

          <!-- In case no image is uploaded -->
          <div v-if="!imageUrl" class="icon-wrapper">
            <img src="@/assets/images/camera.png" alt="camera icon" />
          </div>
          <p v-if="!imageUrl">
            <img src="@/assets/images/Capa 3.png" alt="" style="width: 40px" />
            Tap here to take a photo
          </p>

          <!-- Display uploaded image -->
          <div v-else class="image-wrapper">
            <!-- Frame overlay -->
            <img
              v-if="selectedFrame"
              :src="selectedFrame"
              class="frame-overlay"
              alt="Selected Frame"
            />
            <img :src="imageUrl" class="uploaded-image" alt="Uploaded Image" />
          </div>
          <!-- Button to retake the photo -->
          <div v-if="imageUrl && !selectedFrame" class="retake-button-container">
            <button class="retake-button" @click="resetPhoto">
              <img src="@/assets/images/retake_camera.png" alt="Retake Icon"> Retake
            </button>
          </div>
        </div>
      </div>

      <!-- Frame selection -->
      <div v-if="imageUrl" class="frame-selection">
        <div class="frames">
          <img
            v-for="(frame, index) in frames"
            :key="index"
            :src="frame"
            class="frame-thumbnail"
            :class="{ 'selected-frame': selectedFrame === frame }"
            @click="selectFrame(frame)"
          />
        </div>
      </div>
     </div>
     
  </div>

  <div class="button-container">
    <button class="back-button" v-if="imageUrl" @click="resetPhoto">
      Back
    </button>

    <button
      class="next-button"
      :disabled="!imageUrl"
      @click="goToNext"
      v-if="!selectedFrame"
    >
      Next
    </button>

    <button
      class="print-button"
      v-if="selectedFrame"
      @click="printImageWithFrame"
    >
      Print
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";

//using variables
const imageUrl = ref(null);
const fileInput = ref(null);
const selectedFrame = ref(null);

//frames
import frame1 from "@/assets/images/frame1.png";
import frame2 from "@/assets/images/frame2.png";
import frame3 from "@/assets/images/frame3.png";
import frame4 from "@/assets/images/frame4.png";
import frame5 from "@/assets/images/frame5.png";
import frame6 from "@/assets/images/frame6.png";

// List of frames
const frames = [frame1, frame2, frame3, frame4, frame5, frame6];

// Function to open file input
const openFileInput = () => {
  fileInput.value.click(); // Open file input dialog
};

// Function to handle uploaded photo
const handlePhoto = (event) => {
  const file = event.target.files[0];
  if (file) {
    imageUrl.value = URL.createObjectURL(file);
  }
};

// Function to reset the photo and frame
const resetPhoto = () => {
  imageUrl.value = null;
  selectedFrame.value = null;
};

// Function to select a frame
const selectFrame = (frame) => {
  selectedFrame.value = frame;
  console.log("Selected frame:", selectedFrame.value);
};

// Function to proceed to the next step
const goToNext = () => {
  console.log("Next button clicked, proceed to the next step.");
};

// Function to print the image with frame
const printImageWithFrame = () => {
  window.print();
};
</script>

<style>
body {
  margin: 0;
  display: flex;
  flex-direction: column;
  background-image: url("@/assets/images/Rectangle.png");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  
}

.center-container {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.photo-frame-container {
  display: flex;
  align-items: flex-start;
  gap: 20px;
}

.button-container {
  position: relative;
  top: 80px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
}

.back-button,
.next-button,
.print-button {
  background-color: #7e3493;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 30px;
  cursor: pointer;
  width: 150px;
}
.next-button,.print-button{
  bottom: 20px !important;
    position: absolute;
    right: 20px;
}
.back-button{
  bottom: 20px !important;
    position: absolute;
    left: 20px;
}
.next-button:disabled {
  background-color: #808080;
  cursor: not-allowed;
  position: absolute;
  right: 20px;
}

.photo-container {
  width: 676px; 
  height: 500px;
  border: 3px solid #ffffff;
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
  padding: 20px !important;
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
  width: 100%;
  height: auto;
  position: relative;
}

.uploaded-image {
  width: 100%;
  height: auto;
  /* max-height: 100%; */
  object-fit: cover;
}

.frame-overlay {
  position: absolute;
  z-index: 20;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* object-fit: cover; */
  /* border-radius: 30px;  */
}

.frame-selection {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  right: 120px;
  position: absolute;
  padding: 20px;
}

.frames {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 40px;
}

.frame-thumbnail {
  width: 100px;
  height: 100px;
  background-color: #eaeaea;
  cursor: pointer;
  border: 2px solid transparent;
  border-radius: 10px;
  
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
}

.selected-frame {
  border-color: #7e3493;
}

.frame-thumbnail:hover {
  border-color: #888;
}

.retake-button-container {
  display: flex;
  justify-content: center;
  margin-top: 10px;
  bottom: 5px; 
 
}

.retake-button {
  background-color: white;
  border: 1px solid #a3a3a3;
  padding: 10px 20px;
  color: #7e3493;
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

/* print */

@media print {
  body * {
    visibility: hidden; /* Hide everything */
  }

  .content, .photo-container, .image-wrapper * {
    visibility: visible; /* Only show the content */
  }

  .photo-container {
    position: fixed; 
    top: 50%; 
    left: 50%; 
    transform: translate(-50%, -50%); 
    width: auto; 
    height: auto; 
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
    z-index: 100; 
  }

  .image-wrapper {
    width: auto; 
    display: flex;
    justify-content: center; 
    align-items: center; 
  }

  .uploaded-image {
    max-width: 100%; 
    height: auto; 
    max-height: 100vh; 
    object-fit: cover; 
  }

  .frame-overlay {
    width: 100%;
    height: 100%;
  }
  
}

@media (max-width: 1024px) { /* Target iPad and smaller screens */
  .photo-frame-container {
    display: flex;
    justify-content: space-between; 
    align-items: flex-start;
    gap: 20px;
  }
  .center-container
  {
    margin-top: 120px;
  }

  .photo-container {
    padding: 10px; 
    width: 476px; 
    height: 500px;
    
  }

  .frame-selection {
    display: flex;
    flex-direction: column;
    margin-top: 60px; 
    right: 0; 
    position: relative; 
    padding: 20px;
  }

  .frames {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px; 
  }
}

</style>
