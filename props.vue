<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <p>Step: {{ step }}</p>
  </div>
</template>

<script>
import { defineProps, ref, computed } from 'vue';

export default {
  setup() {
    // // way 1
    const props = defineProps({
      initialCount: {
        type: Number,
        default: 0
      },
      step: {
        type: Number,
        default: 1
      }
    });

    // way 2
    const props = defineProps(['initialCounter'])

    // counter only uses props.initialCounter as the initial value;
    // it is disconnected from future prop updates.
    const counter = ref(props.initialCounter)

    // Define reactive variable for count
    const count = ref(props.initialCount);

    // Increment and decrement methods
    const increment = () => {
      count.value += props.step;
    };

    const decrement = () => {
      count.value -= props.step;
    };

    // Computed property for doubled count
    const doubledCount = computed(() => count.value * 2);

    // Return reactive variables and methods
    return {
      count,
      increment,
      decrement,
      doubledCount
    };
  }
};
</script>
