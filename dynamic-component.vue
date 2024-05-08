<template>
  <div>
    <button @click="toggleComponent">Toggle Component</button>
    <component :is="currentComponent"></component>
  </div>
</template>
  
<script>
import { ref } from 'vue';
import ComponentA from './components/ComponentA.vue';
import ComponentB from './components/ComponentB.vue';

export default {
  setup() {
    const currentComponent = ref('ComponentA');

    const toggleComponent = () => {
      currentComponent.value = currentComponent.value === 'ComponentA' ? 'ComponentB' : 'ComponentA';
    };

    return {
      currentComponent,
      toggleComponent
    };
  },
  components: {
    ComponentA,
    ComponentB
  }
};
</script>
  