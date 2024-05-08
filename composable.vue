// useApi.js (Composable)
import { ref } from 'vue';
import axios from 'axios';

export default function useApi(url) {
  const data = ref(null);
  const loading = ref(false);
  const error = ref(null);

  const fetchData = async () => {
    loading.value = true;
    try {
      const response = await axios.get(url);
      data.value = response.data;
    } catch (err) {
      error.value = err.message;
    } finally {
      loading.value = false;
    }
  };

  return {
    data,
    loading,
    error,
    fetchData
  };
}


<!-- ===== usage ====== -->

<template>
  <div>
    <h1>Data from API</h1>
    <div v-if="loading">Loading...</div>
    <div v-else-if="error">Error: {{ error }}</div>
    <div v-else>
      <ul>
        <li v-for="item in data" :key="item.id">{{ item.title }}</li>
      </ul>
    </div>
    <button @click="fetchData">Fetch Data</button>
  </div>
</template>
  
<script>
import useApi from './useApi';

export default {
  setup() {
    const { data, loading, error, fetchData } = useApi('https://jsonplaceholder.typicode.com/posts');

    return {
      data,
      loading,
      error,
      fetchData
    };
  }
};
</script>
  