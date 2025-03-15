<template>
  <div class="uploader">
    <h2>Upload Image</h2>
    <input type="file" @change="onFileChange" />
    <button @click="uploadImage">Upload</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      selectedFile: null,
    };
  },
  methods: {
    onFileChange(event) {
      this.selectedFile = event.target.files[0];
    },
    async uploadImage() {
      const formData = new FormData();
      formData.append('image', this.selectedFile);
      try {
        await axios.post('https://your-api-domain.com/upload', formData);
        alert('Image uploaded successfully!');
      } catch (error) {
        console.error('Error uploading image:', error);
      }
    },
  },
};
</script>

<style scoped>
.uploader {
  color: #e0e0e0;
  background-color: #3a003c;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #9b59b6;
}
input[type="file"] {
  color: #e0e0e0;
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
</style>
