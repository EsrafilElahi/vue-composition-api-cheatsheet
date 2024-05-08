<!-- watch -->
<script>
import { ref, watch } from 'vue';

export default {
  setup() {
    const message = ref('');

    watch(message, (newVal, oldVal) => {
      console.log('Message changed from', oldVal, 'to', newVal);
    });

    return {
      message
    };
  }
};
</script>
