<script setup>
import { ref, computed } from 'vue'

  let id = 0;

  const newTodo = ref('');
  const hideCompleted = ref(false);
  const hideMessage = ref(generateHideButtonMessage());

  const todos = ref([
    { id: id++, text: "Learn Java Spring", done: true },
    { id: id++, text: "Learn Vue.js", done: false },
    { id: id++, text: "Learn PostgreSQL", done: true }
  ]);

  // computed: create a computed ref that computes its `.value`
  // based on other reactive data sources.
  // A computed property tracks other reactive state used in its computation
  // as dependencies; it automatically updates when its dependencies change.
  const filteredTodos = computed(() => {
    return hideCompleted.value
    ? todos.value.filter(t => !t.done)
    : todos.value;
  })

  function addTodo() {
    const todo = {
        id: id++,
        text: newTodo.value,
        done: false
    };

    todos.value.push(todo);
    clearInput();
  }

  function removeTodo(todo) {
    const index = todos.value.findIndex(t => t.id === todo.id);
    todos.value.splice(index, 1);
  }

  function clearInput() {
    newTodo.value = "";
  }

  function changeTodosDisplay() {
    hideCompleted.value = !hideCompleted.value;
    hideMessage.value = generateHideButtonMessage();
  }

  function generateHideButtonMessage() {
    return hideCompleted.value ? "Show completed tasks" : "Hide completed tasks";
  }

  // define class and Id for CSS style
  const listClass = ref("list");
  const textInputClass = ref("textInput");
  const deleteButtonClass = ref("deleteButton")
</script>

<!-- v-... is a directive = special attribute in Vue -->
<template>
    <!-- @submit.prevent -> prevent from sending the post request -->
    <form @submit.prevent="addTodo">
        <input :class="textInputClass" v-model="newTodo" required placeholder="new Todo">
        <button>Add Todo</button>
    </form>

  <ul :class="listClass" >
    <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done">
        {{ todo.text }}
        <button :class="deleteButtonClass" @click="removeTodo(todo)">X</button>
    </li>
  </ul>

  <button @click="changeTodosDisplay">
        {{ hideMessage }}
  </button>
</template>

<style scoped>
.list {
  font-size: larger;
  color: #317873;
  list-style: none;
}

li {
    margin: 0.5em 0em;
}

button.deleteButton {
    margin-left: 1em;
    padding: 0.2em 0.6em;
    background-color: rgba(206, 32, 41, 0.2);
}
</style>