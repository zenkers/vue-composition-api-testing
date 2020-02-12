<template>
  <button
    ref="incrementButton"
    @click="increment">
    Count is: {{ state.count }}, double is: {{ state.double }}
  </button>
</template>

<script>
import {
  computed,
  onBeforeMount,
  onMounted,
  onUpdated,
  reactive,
  ref,
} from '@vue/composition-api';

export default {
  setup() {
    const incrementButton = ref(null);

    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2),
    });

    function increment() {
      state.count += 1;
    }

    /* eslint-disable no-console */
    console.log('created');

    onBeforeMount(() => {
      console.log('before mounted');
      console.log(incrementButton.value); // null - not available until mounted
    });

    onMounted(() => {
      console.log('mounted');
      console.log(incrementButton.value.innerText);
    });

    onUpdated(() => {
      console.log('updated');
      console.log(incrementButton.value.innerText);
    });
    /* eslint-enable no-console */

    return {
      state,
      increment,
      incrementButton,
    };
  },
};
</script>
