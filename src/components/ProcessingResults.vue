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
.results{

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



.results:hover {
background-color: #2490f5bb;
}
</style>
