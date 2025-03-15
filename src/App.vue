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
  text-align: center;
  background-color: #2c003c;
  min-height: 100vh;
  color: #e0e0e0;
  padding: 20px;
}

.title {
  color: #9b59b6;
  text-shadow: 0 0 20px #9b59b6;
}
</style>

