<template>
  <div>
    <label for="numberInput">Enter a number:</label>
    <input type="text" v-model="number" v-number id="numberInput">
  </div>
</template>
  
<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'MyComponent',
  setup() {
    const number = ref('');

    const numberDirective = (el) => {
      const inputHandler = (event) => {
        const currentValue = event.target.value;
        const sanitizedValue = currentValue.replace(/[^\d]/g, '');
        event.target.value = sanitizedValue;
      };

      el.addEventListener('input', inputHandler);

      onMounted(() => {
        return () => {
          el.removeEventListener('input', inputHandler);
        };
      });
    };

    return {
      number,
      numberDirective
    };
  },
  directives: {
    number: {
      mounted(el, binding) {
        binding.value(el);
      }
    }
  }
};
</script>