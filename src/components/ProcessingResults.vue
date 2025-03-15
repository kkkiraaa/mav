<template>
  <div class="results">
    <h2>Processing Results</h2>
    <div v-if="results">
      <h3>Detected Objects:</h3>
      <ul>
        <li v-for="(object, index) in results.objects" :key="index">{{ object }}</li>
      </ul>
      <h3>Recognized Text:</h3>
      <p>{{ results.text }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      results: null,
    };
  },
  async created() {
    try {
      const response = await axios.get('http://192.168.215.102:8443/results');
      this.results = response.data;
      console.log(this.results);
    } catch (error) {
      console.error('Error fetching results:', error);
    }
  },
};
</script>

<style scoped>
.results {
  color: #e0e0e0;
  background-color:rgba(182, 153, 97, 0.77);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #9b59b6;
  margin-bottom: 20px; 
}
</style>
