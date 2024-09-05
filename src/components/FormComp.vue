<script setup>
  import { ref } from 'vue'

  const text = ref("");

  // arguments received from the parent component;
  // defineProps is a compile-time macro (no need to import it)/
  const props = defineProps({
    argt: String
  });

  // declare emitted events
  const emit = defineEmits(["response"]);
  emit("response", "Emitted message from the child component.");
</script>

<!-- v-... is a directive = special attribute in Vue -->
<!-- v-model replaces v-on: no need for an event listener now -->
<template>
  <p>{{ argt }}</p>

  <input v-model="text" placeholder="Type your text here">

  <p>{{ text }}</p>
</template>

<style scoped>
  input:focus {
  width: 25em;
  transition: all 0.5s ease-in-out;
}
</style>