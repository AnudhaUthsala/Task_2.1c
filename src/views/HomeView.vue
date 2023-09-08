<script setup>
import { ref } from "vue";

const todoId = ref(0);
const todoItem = ref("");
const todoStore = ref([]);
const completed = ref(false);

function addItems() {
  todoStore.value.push({
    id: todoId.value++,
    items: todoItem.value,
    status: completed.value,
  });

  todoItem.value = "";
}

function toggleCompleted(idToFind) {
  const todo = this.todoStore.find((obj) => obj.id === idToFind);

  if (todo.status) {
    todo.status = false;
  } else {
    todo.status = true;
  }
}

function deleteTodo(idFind) {
  this.todoStore = this.todoStore.filter((item) => item.id !== idFind);
}
</script>

<template>
  <div class="todo-app">
    <header>
      <h1 class="header">Todo List</h1>
    </header>
    <main>
      <div class="add-todo">
        <input type="text" placeholder="Add a New Todo" v-model="todoItem" />
        <button @click="addItems">Add</button>
      </div>
      <ol class="todo-list">
        <li
          v-for="i in todoStore"
          :key="i.id"
          class="todo"
          :class="{ completedDo: i.status }"
        >
          <label class="checkbox">
            <input type="checkbox" @click="toggleCompleted(i.id)" />
            <span class="checkbox-custom"></span>
          </label>
          <span :class="{ completed: i.status }" class="todo-text">{{
            i.items
          }}</span>
          <button class="delete-button" @click="deleteTodo(i.id)">
            Delete
          </button>
        </li>
      </ol>
    </main>
  </div>
</template>

<style scoped>
.todo-app {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
  align-items: center;
}

.header {
  font-size: 50px;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-todo input[type="text"] {
  flex: 1;
  padding: 8px;
  height: 40px;
  font-size: 25px;
}

.add-todo button {
  padding: 8px 12px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100px;
  font-size: 25px;
}

.add-todo button:hover {
  background-color: green;
  color: #fff;
  transform: scale(1.05);
}

.todo-list {
  list-style: none;
  padding: 0;
  cursor: pointer;
}

.todo {
  display: flex;
  align-items: center;
  padding: 10px;
  background-color: #dbe9fa;
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

.todo input[type="checkbox"] {
  margin-right: 10px;
}

.todo-text {
  flex: 1;
  font-size: 30px;
  font-weight: 700;
}

.delete-button {
  padding: 6px 12px;
  background-color: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100px;
  height: 40px;
  font-weight: 600;
}

.completed {
  text-decoration: line-through;
  color: #778899;
  font-weight: 200;
}

/* Media Queries */
@media screen and (max-width: 480px) {
  .todo-app {
    padding: 10px;
  }

  .add-todo {
    flex-direction: column;
    gap: 5px;
  }

  .add-todo input[type="text"] {
    width: 100%;
  }
}
</style>
