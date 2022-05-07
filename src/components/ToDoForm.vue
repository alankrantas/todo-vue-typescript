<template>
  <form ref="addToDoForm" @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo-input" class="label__lg">
        What needs to be done?
      </label>
    </h2>
    <input
      type="text"
      id="new-todo-input"
      name="new-todo"
      autocomplete="off"
      v-model.lazy.trim="newLabel"
      class="input__lg"
    />
    <button type="submit" class="btn btn__primary btn__lg">
      <span class="visually-hidden">Add task</span>
      <img :src="`./icons8-add-new-24.png`" />
    </button>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";

const newLabel = ref<string>("");
const addToDoForm = ref(null);

const emit = defineEmits<{
  (e: "todo-added", label: string): void;
}>();

const onSubmit = () => {
  if (newLabel.value !== "") {
    emit("todo-added", newLabel.value);
    newLabel.value = "";
    addToDoForm.value.reset();
  }
};
</script>

<style scoped>
.label-wrapper {
  margin: 0;
  flex: 0 0 100%;
  text-align: center;
}
.label__lg {
  line-height: 1.01567;
  font-weight: 300;
  padding: 0.8rem;
  margin-bottom: 1rem;
  text-align: center;
}
.input__lg {
  padding: 2rem;
  border: 2px solid black;
}
.input__lg:focus {
  border-color: grey;
  box-shadow: inset 0 0 0 2px;
}
[class*="__lg"] {
  display: inline-block;
  width: 100%;
  font-size: 1.9rem;
}
[class*="__lg"]:not(:last-child) {
  margin-bottom: 1rem;
}
</style>