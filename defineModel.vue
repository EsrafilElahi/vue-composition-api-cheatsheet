<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <p>Step: {{ step }}</p>
  </div>
</template>
  
<script>
import { defineProps, defineEmits, ref, computed } from 'vue';

export default {
  emits: ['update:modelValue'],

  setup(props, { emit }) {
    // Define props
    const { initialCount, step } = defineProps({
      initialCount: {
        type: Number,
        default: 0
      },
      step: {
        type: Number,
        default: 1
      }
    });

    // Define reactive variable for count
    const count = ref(initialCount);

    // Increment and decrement methods
    const increment = () => {
      count.value += step;
      emit('update:modelValue', count.value);
    };

    const decrement = () => {
      count.value -= step;
      emit('update:modelValue', count.value);
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
  

<!-- ===== another exmaple ====== -->

<!-- Child.vue -->
<script setup>
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])
</script>

<template>
  <input :value="props.modelValue" @input="emit('update:modelValue', $event.target.value)" />
</template>

<!-- Parent.vue -->
<Child
  :modelValue="foo"
  @update:modelValue="$event => (foo = $event)"
/>