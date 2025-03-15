<template>
  <div class="search">
    <h2>Search Images</h2>
    <input v-model="searchQuery" placeholder="Enter metadata..." />
    <button @click="searchImages">Search</button>
    <div v-if="images.length">
      <h3>Results:</h3>
      <ul>
        <li v-for="(image, index) in images" :key="index">
          {{ image.metadata }} <button @click="downloadImage(image.id)">Download</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      searchQuery: '',
      images: [],
    };
  },
  methods: {
    async searchImages() {
      try {
        const response = await axios.get(`http://192.168.96.102:8443/search?query=${this.searchQuery}`);
        this.images = response.data;
      } catch (error) {
        console.error('Error searching images:', error);
      }
    },
    async downloadImage(imageId) {
     try {
        const response = await axios.get(`http://192.168.96.102:8443/download/${imageId}`, {
          responseType: 'blob', // Important for downloading files
        });
        const url = window.URL.createObjectURL(new Blob([response.data]));
        const link = document.createElement('a');
        link.href = url;
        link.setAttribute('download', `image_${imageId}.jpg`); // Change the file name as needed
        document.body.appendChild(link);
        link.click();
        link.remove();
      } catch (error) {
        console.error('Error downloading image:', error);
      }
    },
  },
};
</script>

<style scoped>
.search {
  color: #e0e0e0;
  background-color:rgb(246, 223, 178, 0.77);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #9b59b6;
}
input {
  color: #e0e0e0;
  background-color: #4a004a;
  border: none;
  padding: 10px;
  border-radius: 5px;
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
