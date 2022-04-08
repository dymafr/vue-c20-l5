<template>
  <div class="p-20 d-flex justify-content-center">
    <div class="card container">
      <h1 class="mb-20">Todo List</h1>
      <div class="d-flex align-items-center">
        <input v-model="input" type="text" class="flex-fill mr-20" />
        <button class="btn btn-primary mr-20" @click="addTodo">Ajouter</button>
      </div>
      <ul>
        <li
          @click="toggleTodo(index)"
          v-for="(todo, index) in todos"
          class="card d-flex align-items-center"
          :key="todo.content"
        >
          <input class="mr-20" :checked="todo.done" type="checkbox" />
          <span class="flex-fill">{{ todo.content }}</span>
          <button @click.stop="deleteTodo(index)" class="btn btn-danger">
            Supprimer
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useTodos } from './stores/todoStore';

const input = ref<string>('');

const todoStore = useTodos();
const todos = todoStore.todoList;

function addTodo() {
  todoStore.addTodo(input.value);
  input.value = '';
}

function deleteTodo(index: number) {
  todoStore.deleteTodo(index);
}

function toggleTodo(index: number) {
  todoStore.toggleTodo(index);
}
</script>

<style lang="scss">
@import './assets/scss/base.scss';

.container {
  width: 500px;
}

li {
  margin-bottom: 20px;
  cursor: pointer;
}
</style>
