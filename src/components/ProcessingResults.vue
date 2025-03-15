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
      const response = await axios.get('https://your-api-domain.com/results');
      this.results = response.data;
    } catch (error) {
      console.error('Error fetching results:', error);
    }
  },
};
</script>

<style scoped>
.results {
  color: #e0e0e0;
  background-color: #3a003c;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px #9b59b6;
}
</style>
