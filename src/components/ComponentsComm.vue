<script setup>
  import { ref } from 'vue'

  // arguments received from the parent component;
  // defineProps is a compile-time macro (no need to import it)/
  const props = defineProps({
    argt: String
  });

  // declare emitted events
  const emit = defineEmits(["response"]);
  emit("response", "Emitted message from the child component.");

  const parentComponentClass = ref("parent-component");
</script>

<!-- v-... is a directive = special attribute in Vue -->
<!-- v-model replaces v-on: no need for an event listener now -->
<template>
  <p :class="parentComponentClass">{{ argt }}</p>
  <slot>Fallback content</slot>
</template>