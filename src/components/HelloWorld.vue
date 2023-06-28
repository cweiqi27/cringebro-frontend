<script setup lang="ts">
import { ref, watch } from "vue";

const todoId = ref(0);
const todoData = ref(null);

const fetchData = async () => {
  todoData.value = null;
  const res = await fetch(`https://rickandmortyapi.com/api/character/${todoId.value},22`);
  todoData.value = await res.json();
};

fetchData();

watch(todoId, fetchData);
</script>

<template>
  <div class="greetings">
    <button @click="todoId++">fetch next todo</button>
    <h1>
      {{ todoId }}
    </h1>
    <p v-if="!todoData">Loading...</p>
    <p v-else>
      {{ todoData }}
    </p>
  </div>
</template>

<style scoped>
#reverse {
  color: red;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
