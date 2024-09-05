<script setup>
import { ref, onMounted } from 'vue'

  const pElementRef = ref(null);
  const btnElementRef = ref(null);

  const isDisabled = ref(false);

  onMounted(() => {
    pElementRef.value.textContent = "DOM has changed after the component has been mounted!";
  });

  function disableButton() {
    isDisabled.value = true;
  }

  const untouchedClass = ref("untouched");
  const changedClass = ref("changed");
</script>

<template>
  <p :id="untouchedClass">
    DOM untouched.
  </p>
  <p :id="changedClass" ref="pElementRef">
    DOM changed before mounted.
  </p>

  <button ref="btnElementRef" :disabled="isDisabled" @click="disableButton">
    Click to disable
  </button>
  <p v-if="isDisabled">Button is disabled.</p>
</template>

<style scoped>
  #untouched {
    font-weight: 600;
  }

  #changed {
    font-style: italic;
  }

  button:disabled {
    background-color: gray;
  }
</style>