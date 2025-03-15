<template>
  <div id="app">
    <h1 class="title">Image Processing Interface</h1>
    <ImageUploader />
    <ProcessingResults />
    <ImageSearch />
  </div>
</template>

<script>
import ImageUploader from './components/ImageUploader.vue';
import ProcessingResults from './components/ProcessingResults.vue';
import ImageSearch from './components/ImageSearch.vue';

export default {
  components: {
    ImageUploader,
    ProcessingResults,
    ImageSearch,
  },
};
</script>

<style>
#app {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-image: url("C:\Users\ASUS\Desktop\app\src\assets\фон.jpeg"); 
  background-size: cover; 
  background-repeat: no-repeat; 
  background-position: center center;
  background-attachment: fixed; 
  color: #e0e0e0;
  text-align: center;
}

.title {
  color: #17e5bf;
  text-shadow: 0 0 20px #10b4cabd;
}

</style>
