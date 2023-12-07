<script setup>
import { ref, onMounted, computed, watch } from "vue";
const todos = ref([]);
const name = ref(``);

const input_content = ref(``);
const input_category = ref(null);
const todos_arr = computed(() =>
  todos.value.sort((a, b) => {
    return a.createdAt - b.createdAt;
  })
);

watch(name, (nameVal) => {
  localStorage.setItem("name", nameVal);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
});

const addToDo = () => {};
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h2 class="title">
        Whats up??<input type="text" placeholder="name here" v-model="name" />
      </h2>
    </section>
    <section class="create-todo">
      <h3>Create a todo</h3>
      <form @submit.prevent="addToDo">
        <h1>Whats on your todoList??</h1>
        <input type="text" placeholder="learn vue js" v-model="input_content" />

        <h2>Pick a category</h2>
        <div class="options">
          <label>
            <input
              type="radio"
              name="category"
              id="category1"
              value="business"
              v-model="input_category"
            />
            <span class="bubble business"></span>
            <div>Business</div>
          </label>

          <label>
            <input
              type="radio"
              name="category"
              id="category1"
              value="personal"
              v-model="input_category"
            />
            <span class="bubble personal"></span>
            <div>Personal</div>
          </label>
        </div>

        <input type="submit" value="Add todo" />
      </form>
    </section>
  </main>
</template>
