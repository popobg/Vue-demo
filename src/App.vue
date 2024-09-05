<script setup>
import { ref } from 'vue'
import FormComp from './components/FormComp.vue'
import ButtonComp from './components/ButtonComp.vue'
import Todo from './components/Todo.vue'
import ChangeDOM from './components/ChangeDOM.vue'
import ComponentsComm from './components/ComponentsComm.vue'

  const message = ref("Welcome to my Vue demo");
  const messageFromParent = ref("Props message from the parent component.");
  const messageFromChild = ref("");
  const msg = ref('from parent, display in the slot');

  const componentClass = ref("component");
  const flexComponentsClass = ref("flex-components");
  const commentClass = ref("comment");
  const childComponentId = ref("child-component");
  const parentComponentClass = ref("parent-component");
</script>

<!-- v-... is a directive = special attribute in Vue -->
<template>
  <h1>{{ message }}</h1>
  <em>Every boxes are distinct Vue components.</em>

  <div :class="flexComponentsClass">
    <div :class="componentClass">
      <div>
        <h2>Event listener</h2>
        <p :class="commentClass">Button test, dynamic incrementation, watchers and conditional rendering</p>
      </div>
      <hr />
      <ButtonComp />
    </div>

    <div :class="componentClass">
      <div>
        <h2>Form binding</h2>
        <p :class="commentClass">Input test with v-model directive</p>
      </div>
      <hr />
      <FormComp />
    </div>

    <div :class="componentClass">
      <div>
        <h2>Lifecycle and template refs</h2>
        <p :class="commentClass">Change DOM after content has been mounted</p>
      </div>
      <hr />
      <ChangeDOM />
    </div>
  </div>

  <div :class="componentClass">
    <div>
      <h2>Todo list</h2>
      <p :class="commentClass">Todo list experiencing functions, iteration with Vue directive, computed properties and checkboxes</p>
    </div>
    <hr />
    <Todo />
  </div>

  <div :class="componentClass">
    <div>
      <h2>Exchanges between parent/child components</h2>
      <p :class="commentClass">Props/emits between parent and child components + part of component exchange using slot</p>
    </div>
    <hr />
    <ComponentsComm :argt="messageFromParent" @response="(msg) => messageFromChild = msg">
      <p :class="parentComponentClass">Message {{ msg }}</p>
    </ComponentsComm>
    <p :id="childComponentId">{{ messageFromChild }}</p>
  </div>
</template>

<style>
.component {
  border:#24292E solid 0.2em;
  border-radius: 0.5em;
  margin: 1em;
  padding: 2em;
  width: fit-content;

  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.flex-components {
  display: flex;
  flex-direction: row;
}

.comment {
  font-style: italic;
  color: #B8860B;
}

.parent-component{
  color: #A81C07;
}

#child-component {
  color: #26619C;
}
</style>