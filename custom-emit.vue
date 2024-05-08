<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup(_, { emit }) {
    const emitEvent = () => {
      emit('custom-event', 'Hello from child component');
    };

    return {
      emitEvent
    };
  }
});
</script>

<!-- ==== usage ==== -->

<script>
import { onMounted } from 'vue';

export default {
  props: ['parentData'],
  setup(props) {
    onMounted(() => {
      console.log('Parent data:', props.parentData);
    });
  }
};
</script>
