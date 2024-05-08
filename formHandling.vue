<template>
  <div>
    <h1>Form Handling with Validation</h1>
    <form @submit.prevent="submitForm">
      <div>
        <label for="username">Username:</label>
        <input type="text" id="username" v-model="formData.username" required>
        <span v-if="!formData.username" style="color: red;">Username is required</span>
      </div>
      <div>
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="formData.password" required>
        <span v-if="!formData.password" style="color: red;">Password is required</span>
      </div>
      <button type="submit" :disabled="!isFormValid">Submit</button>
    </form>
  </div>
</template>
  
<script>
import { reactive, computed } from 'vue';

export default {
  setup() {
    // Define reactive form data
    const formData = reactive({
      username: '',
      password: ''
    });

    // Compute form validation
    const isFormValid = computed(() => {
      return formData.username && formData.password;
    });

    // Form submission handler
    const submitForm = () => {
      if (isFormValid.value) {
        // Form is valid, submit data
        console.log('Submitting form:', formData);
      } else {
        // Form is not valid, display error
        console.error('Form is not valid');
      }
    };

    return {
      formData,
      isFormValid,
      submitForm
    };
  }
};
</script>
  