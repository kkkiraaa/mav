<template>
  <div class="uploader">
    <h2>Upload Image</h2>
    <input type="file" @change="onFileChange" />
    <button @click="uploadImage">Upload</button>
    
    <!-- Display the uploaded image and bounding boxes -->
    <div class="image-container" v-if="imageUrl">
      <img :src="imageUrl" alt="Uploaded Image" class="uploaded-image" />
      <div class="bounding-box" 
           v-for="(bbox, index) in boundingBoxes" 
           :key="index" 
           :style="getBoundingBoxStyle(bbox)">
      </div>
    </div>

    <!-- Display the response data -->
    <div v-if="responseData" class="response-container">
      <h3>Response Data:</h3>
      <pre>{{ responseData }}</pre> <!-- Display the JSON response -->
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      selectedFile: null,
      responseData: null,
      imageUrl: null, // To store the uploaded image URL
      boundingBoxes: [], // To store bounding box data
    };
  },
  methods: {
    onFileChange(event) {
      this.selectedFile = event.target.files[0];
    },
    async uploadImage() {
      const formData = new FormData();
      formData.append('file', this.selectedFile);
      formData.append('apiUrl', "https://16af-35-237-206-107.ngrok-free.app/process-image");
      
      try {
        const response = await axios.post('http://192.168.96.102:8443/images/upload-to-api', formData);
        this.responseData = response.data; // Store the response data
        this.imageUrl = URL.createObjectURL(this.selectedFile); // Create a URL for the uploaded image
        this.boundingBoxes = this.parseBoundingBoxes(response.data.bboxes); // Parse bounding boxes
        alert('Image uploaded successfully!');
      } catch (error) {
        console.error('Error uploading image:', error);
      }
    },
    parseBoundingBoxes(bboxes) {
      return bboxes.map(bbox => {
        const coords = JSON.parse(bbox); // Parse the string to get coordinates
        return {
          left: coords[0] * 100 + '%', // Convert to percentage
          top: coords[1] * 100 + '%', // Convert to percentage
          width: (coords[2] - coords[0]) * 100 + '%', // Calculate width
          height: (coords[3] - coords[1]) * 100 + '%', // Calculate height
        };
      });
    },
    getBoundingBoxStyle(bbox) {
      return {
        position: 'absolute',
        border: '2px solid red',
        left: bbox.left,
        top: bbox.top,
        width: bbox.width,
        height: bbox.height,
        pointerEvents: 'none', // Prevent interaction with the bounding box
      };
    },
  },
};
</script>

<style scoped>
.uploader {
  color: #e0e0e0;
  background-color: rgba(246, 223, 178, 0.77);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #9b59b6;
}

input[type="file"] {
  color: #e0e0e0;
  margin-bottom: 20px; 
}

button {
  background-color: #8e44ad;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #732d91;
}

.image-container {
  position: relative; /* Позиционирование для наложения bounding boxes */
}

.uploaded-image {
  max-width: 100%; /* Адаптивное изображение */
  height: auto;
}

.bounding-box {
  position: absolute; /* Позиционирование для наложения на изображение */
  border: 2px solid red; /* Цвет и стиль рамки */
  pointer-events: none; /* Отключение взаим  одействия с рамкой */
}
response-container {
  background-color: rgba(246, 223, 178, 0.5); /* Полупрозрачный фон для контейнера с ответом */
  border: 1px solid #9b59b6; /* Рамка вокруг контейнера */
  border-radius: 5px; /* Закругленные углы */
  padding: 10px; /* Отступы внутри контейнера */
  margin-top: 20px; /* Отступ сверху для отделения от изображения */
  color: #e0e0e0; /* Цвет текста */
  overflow: auto; /* Прокрутка, если содержимое превышает размер контейнера */
  max-height: 200px; /* Максимальная высота контейнера для ограничения размера */
}
</style>
