<script>
import { provide } from 'vue';

export default {
  setup() {
    provide('sharedData', 'Hello from parent component');
  }
};
</script>

<!-- ==== usage ==== -->

<script>
import { inject, onMounted } from 'vue';

export default {
  setup() {
    const parentData = inject('sharedData');

    onMounted(() => {
      console.log('Parent data:', parentData);
    });
  }
};
</script>
