<!-- watch -->
<script>
import { ref, watch, onMounted, onUnmounted } from 'vue';

export default {
  setup() {
    const message = ref('');

    watch(message, (newVal, oldVal) => {
      console.log('Message changed from', oldVal, 'to', newVal);
    });

    onMounted(() => {
      console.log('Component mounted');
    });

    onUnmounted(() => {
      console.log('Component unmounted');
    });

    return {
      message
    };
  }
};
</script>
