<template>
  <form
    ref="editToDoForm"
    class="stack-small"
    @submit.prevent="emit('item-edited', id, newLabel)"
  >
    <div>
      <label class="edit-label">Edit task for &quot;{{ label }}&quot;</label>
      <input
        :id="id"
        type="text"
        autocomplete="off"
        v-model.lazy.trim="newLabel"
        @vnode-mounted="({ el }) => el.focus()"
        @keyup.enter="onSubmit"
        @keyup.escape="emit('edit-cancelled')"
      />
    </div>
    <div class="btn-group">
      <button type="button" class="btn" @click="emit('edit-cancelled')">
        <img :src="`./icons8-cancel-24.png`" />
        <span class="visually-hidden">Cancel editing {{ label }} </span>
      </button>
      <button type="submit" class="btn btn__primary">
        <img :src="`./icons8-done-24.png`" />
        <span class="visually-hidden">Save edit for {{ label }}</span>
      </button>
    </div>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface ToDoItemData {
  id: string;
  label: string;
  done: boolean;
}

const props = defineProps<ToDoItemData>();
const newLabel = ref<string>(props.label);

const emit = defineEmits<{
  (e: "item-edited", id: string, newLabel: string): void;
  (e: "edit-cancelled"): void;
}>();
</script>

<style scoped>
.edit-label {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #0b0c0c;
  display: block;
  margin-bottom: 5px;
}
input {
  display: inline-block;
  margin-top: 0.4rem;
  width: 100%;
  min-height: 4.4rem;
  padding: 0.4rem 0.8rem;
  border: 2px solid #565656;
}
form {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
form > * {
  flex: 0 0 100%;
}
</style>