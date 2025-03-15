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
        const response = await axios.get(`https://your-api-domain.com/search?query=${this.searchQuery}`);
        this.images = response.data;
      } catch (error) {
        console.error('Error searching images:', error);
      }
    },
    async downloadImage(imageId) {
     try {
        const response = await axios.get(`https://your-api-domain.com/download/${imageId}`, {
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
  text-shadow: 0 0 20px #9b59b6;
  transition: background-color 0.3s ease;
}

.search:hover {
  background-color: #2490f5bb;
}
a.searchn {
  display: inline-block;
}
.input {
  display: inline-block;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  background-color: #6ecdf586;
  color: #ffffff;
  border: none;
  border-radius: 8px;

  transition: background-color 0.3s ease;
}
.input:hover {
  background-color: #2490f5bb;
}
.input:active {
  background-color: #0b6db9;
  transform: translateY(2px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); 
}
a.input {
  display: inline-block;}
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
