<template>
  <h1 class="text-center mt-3">Todo List</h1>
  <div
    class="col-10 offset-1 col-md-8 offset-md-2 col-xl-6 offset-xl-3 p-0 my-4"
  >
    <div class="d-flex">
      <input
        v-model="newTodo"
        @keyup.enter="onEnter"
        name="newTodo"
        type="text"
        class="col-10 col-xl-11 border-right-0"
        placeholder="Add a new todo..."
      />

      <button
        @click.prevent="addNewTodo"
        class="col-2 col-xl-1 bg-primary text-white rounded-right d-flex align-items-center justify-content-center m-0 p-0 pointer"
      >
        Add
      </button>
    </div>
    <ul class="my-4 mx-0 p-0">
      <li
        v-for="(todo, index) in todos"
        :key="todo.id"
        class="d-flex border border-dark rounded my-4 py-1 px-3"
      >
        <div class="col-lg-11 col-10 m-0 p-0">
          <h3 :class="{ done: todo.done }">{{ todo.content }}</h3>
        </div>
        <div
          class="col-lg-1 col-2 d-flex m-0 p-0 justify-content-between align-items-center"
        >
          <span @click="toggleDone(todo)"
            ><i class="far fa-check-circle text-success pointer"></i
          ></span>
          <span @click="removeTodo(index)"
            ><i class="far fa-trash-alt text-danger pointer"></i
          ></span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");

    const todos = ref([]);

    let todoIdTracker = 0;

    const addNewTodo = () => {
      todos.value.push({
        id: todoIdTracker,
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
      todoIdTracker++;
    };

    const toggleDone = (todo) => {
      todo.done = !todo.done;
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    const onEnter = () => {
      addNewTodo();
    };

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      onEnter,
    };
  },
};
</script>

<style>
.pointer {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
