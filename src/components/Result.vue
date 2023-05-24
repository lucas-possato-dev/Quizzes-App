<script setup>
import { RouterLink } from "vue-router";
const { quizQuestionLength, correctAnswers } = defineProps([
  "quizQuestionLength",
  "correctAnswers",
]);
</script>

<template>
  <div class="results">
    <p>Você acertou...</p>
    <h1>{{ correctAnswers }}/{{ quizQuestionLength }}</h1>
    <div>
      <RouterLink class="back" to="/">Voltar</RouterLink>
    </div>
  </div>
</template>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0;
  display: flex;
  flex-direction: column;
  gap: 50px;
}

.back {
  padding: 10px 15px;
  background: bisque;
  border-radius: 4px;
  color: inherit;
  font-size: small;
  text-decoration: none;
  transition: all 150ms ease-out;
}

.back:hover {
  background: rgb(241, 206, 162);
}

p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>
