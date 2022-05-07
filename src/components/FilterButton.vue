<template>
  <div class="filter btn-group stack-exception">
    <button
      v-for="name in filterNames"
      :key="name"
      :id="name"
      type="button"
      class="btn toggle-btn"
      :aria-pressed="name === filterSelected"
      @click="emit('set-filter', name)"
    >
      <span class="visually-hidden">Show </span>
      <span>{{ name }}</span>
      <span class="visually-hidden"> tasks</span>
    </button>
  </div>
</template>

<script setup lang="ts">
interface Props {
  filterNames: string[];
  filterSelected: string;
}

defineProps<Props>();

const emit = defineEmits<{
  (e: "set-filter", name: string): void;
}>();
</script>

<style scoped>
.btn.toggle-btn {
  color: gray;
  background-color: lightgoldenrodyellow;
  border-color: lightgray;
}
.btn.toggle-btn[aria-pressed="true"] {
  color: white;
  background-color: darkslategray;
  border-color: darkslategray;
}
.btn.toggle-btn:focus {
  outline-color: lightgoldenrodyellow;
}
</style>