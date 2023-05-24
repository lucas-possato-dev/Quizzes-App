<script setup>
import q from "../data/quizes.json";
import { ref, watch } from "vue";
import Card from "../components/Card.vue";

const quizes = ref(q);
const search = ref("");

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<template>
  <header>
    <h1>Quizzes</h1>
    <input v-model.trim="search" type="text" placeholder="Pesquisar..." />
  </header>
  <div class="options-container">
    <Card v-for="quiz in quizes" :quiz="quiz" />
    <p class="notFound" v-if="quizes.length === 0">No quizzes found...</p>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #b9b5b5;
  outline: none;
  color: rgba(128, 128, 128, 0.7);
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

@media (max-width: 660px) {
  .options-container {
    justify-content: center;
    align-items: center;
  }
}

.notFound {
  font-weight: bold;
  font-size: large;
}
</style>
