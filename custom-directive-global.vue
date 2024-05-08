// main.js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);

// Custom directive
app.directive('uppercase', {
  mounted(el) {
    el.addEventListener('input', function(event) {
      event.target.value = event.target.value.toUpperCase();
    });
  }
});

app.mount('#app');


<template>
  <div>
    <label for="inputField">Enter Text:</label>
    <input type="text" v-uppercase id="inputField">
  </div>
</template>
  
<script>
export default {
  name: 'MyComponent'
};
</script>
  