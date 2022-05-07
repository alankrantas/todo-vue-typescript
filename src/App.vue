<template>
  <div id="app">
    <h1>To-Do List</h1>
    <ToDoForm @todo-added="addToDo" />
    <Transition name="fade">
      <section v-show="ToDoItems.length">
        <FilterButton
          :filterNames="filterNames"
          :filterSelected="filter"
          @set-filter="setFilter"
        />
        <h2 id="list-summary">{{ listSummary }}</h2>
        <TransitionGroup
          name="list"
          tag="ul"
          aria-labelledby="list-summary"
          class="stack-large stack-exception"
        >
          <li v-for="item in filteredToDoItems" :key="item.id">
            <ToDoItem
              :id="item.id"
              :label="item.label"
              :done="item.done"
              @checkbox-changed="updateDoneStatus"
              @item-edited="editToDo"
              @item-deleted="deleteToDo"
            />
          </li>
        </TransitionGroup>
      </section>
    </Transition>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref, computed } from "vue";
import ToDoItem from "./components/ToDoItem.vue";
import ToDoForm from "./components/ToDoForm.vue";
import FilterButton from "./components/FilterButton.vue";
import uniqueId from "lodash.uniqueid";

interface ToDoItemData {
  id: string;
  label: string;
  done: boolean;
}

const ToDoItems = reactive<ToDoItemData[]>([
  {
    id: uniqueId("todo-"),
    label: "Learn JavaScript",
    done: true,
  },
  {
    id: uniqueId("todo-"),
    label: "Understand TypeScript",
    done: true,
  },
  {
    id: uniqueId("todo-"),
    label: "Build Website with Vue.js",
    done: false,
  },
]);

const filterMap = {
  All: () => true,
  Active: (item: ToDoItemData) => !item.done,
  Completed: (item: ToDoItemData) => item.done,
};

const filterNames: string[] = Object.keys(filterMap);
const filter = ref<string>("All");

const filteredToDoItems: ToDoItemData[] = computed(() => {
  return ToDoItems.filter(filterMap[filter.value]);
});

const listSummary: string = computed(() => {
  const completedTasks = ToDoItems.filter(filterMap.Completed).length;
  const tasksNoun = ToDoItems.length > 1 ? "tasks" : "task";
  return `${completedTasks} of ${ToDoItems.length} ${tasksNoun} completed`;
});

const setFilter = (name: string) => {
  filter.value = name;
};

const addToDo = (newLabel: string) => {
  ToDoItems.push({
    id: uniqueId("todo-"),
    label: newLabel,
    done: false,
  });
};

const editToDo = (id: string, newLabel: string) => {
  const toDoToEdit = ToDoItems.find((item) => item.id === id) as ToDoItemData;
  toDoToEdit.label = newLabel;
};

const updateDoneStatus = (id: string) => {
  const toDoToUpdate = ToDoItems.find(
    (item: ToDoItemData) => item.id === id
  ) as ToDoItemData;
  toDoToUpdate.done = !toDoToUpdate.done;
};

const deleteToDo = (id: string) => {
  const itemIndex = ToDoItems.findIndex((item) => item.id === id);
  ToDoItems.splice(itemIndex, 1);
};
</script>

<style>
/* Transition styles */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.25s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
}
.list-leave-active {
  position: absolute;
}
/* Global styles */
.btn {
  padding: 0.8rem 1rem 0.7rem;
  color: white;
  border: 0.2rem solid teal;
  background-color: teal;
  cursor: pointer;
  text-transform: capitalize;
}
.btn:focus {
  outline-color: cadetblue;
}
.btn__primary {
  color: white;
  background-color: steelblue;
  border-color: steelblue;
}
.btn__primary:focus {
  outline-color: lightsteelblue;
}
.btn__danger {
  color: white;
  background-color: indianred;
  border-color: indianred;
}
.btn__danger:focus {
  outline-color: firebrick;
}
.btn-group {
  display: flex;
  justify-content: space-between;
}
.btn-group > * {
  flex: 1 1 49%;
}
.btn-group > * + * {
  margin-left: 0.8rem;
}
@media screen and (min-width: 620px) {
  [class*="__lg"] {
    font-size: 2.4rem;
  }
}
.filters {
  width: 100%;
  margin: unset auto;
}
.visually-hidden {
  position: absolute;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px);
  clip: rect(1px, 1px, 1px, 1px);
  clip-path: rect(1px, 1px, 1px, 1px);
  white-space: nowrap;
}
[class*="stack"] > * {
  margin-top: 0;
  margin-bottom: 0;
}
.stack-small > * + * {
  margin-top: 1.25rem;
}
.stack-large > * + * {
  margin-top: 2.5rem;
}
@media screen and (min-width: 550px) {
  .stack-small > * + * {
    margin-top: 1.4rem;
  }
  .stack-large > * + * {
    margin-top: 2.8rem;
  }
}
.stack-exception {
  margin-top: 1.2rem;
}
/* End global styles */
#app {
  background: whitesmoke;
  margin: 2rem 0 4rem 0;
  padding: 1rem;
  padding-top: 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 2.5rem 5rem 0 rgba(0, 0, 0, 0.1);
}
@media screen and (min-width: 550px) {
  #app {
    padding: 4rem;
  }
}
#app > * {
  max-width: 50rem;
  margin-left: auto;
  margin-right: auto;
}
#app > form {
  max-width: 100%;
}
#app h1 {
  display: block;
  min-width: 100%;
  width: 100%;
  text-align: center;
  margin: 0;
  margin-bottom: 1rem;
}
</style>