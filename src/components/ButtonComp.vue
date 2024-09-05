<script setup>
import { ref, watch } from 'vue'

  const clicked = ref(false);
  // as we are initializing count as a constante,
  // we can modify count.value, but not count itself.
  const count = ref(0);

  function modify() {
    count.value ++;
    clicked.value = true;
  }

  // side effects performed reactively;

  watch(count, (newCount) => {
    console.log("Current count is ", newCount);
  });

  // define Id for CSS style
  const btnId = ref("btn");
</script>

<template>
  <p>
    {{ count }}
  </p>

  <button :id="btnId" @click=modify()>
    Click here
  </button>
  <p v-if="clicked">{{ `I just clicked the button ${count} time(s).` }}</p>
  <p v-else>I haven't clicked on the button yet.</p>
</template>

<style>
#btn {
  border: rgba(248, 222, 126) 0.3em solid;
  border-radius: 10%;

  box-sizing: content-box;
}
</style>