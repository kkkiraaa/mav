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

display: inline-block;
padding: 12px 24px;
width: 450px;
height: 140px;
text-align: center;
text-decoration: none;
cursor: pointer;

background-color: #6ecdf586;
color: #ffffff;
border: none;
border-radius: 8px;

transition: background-color 0.3s ease;
}

.uploader:hover {
background-color: #2490f5bb;
}
input[type="file"] {
  color: #e0e0e0;
}
button {
  display: inline-block;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  border: none;
  border-radius: 8px;
  transition: background-color 0.3s ease;
  background-color: #8e44ad;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}
button:hover {
  background-color: #a449efc0;
}
button:active {
  background-color: #7114bdc0;
  transform: translateY(2px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); 
}
</style>
