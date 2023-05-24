<script setup>
import { useRouter } from "vue-router";

const router = useRouter();
const { quiz } = defineProps(["quiz"]);

const navigateToQuiz = () => {
  router.push(`/quiz/${quiz.id}`);
};
</script>

<template>
  <div class="card" @click="navigateToQuiz">
    <img :src="quiz.img" :alt="quiz.name" />
    <div class="card-text">
      <h2>{{ quiz.name }}</h2>
      <p>{{ quiz.questions.length }} questões</p>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 310px;
  overflow: hidden;
  border-radius: 2%;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 35px;
  margin-right: 20px;
  cursor: pointer;
  transition: all 300ms ease-in-out;
}

.card:hover {
  transform: scale(1.03);
  background: rgb(41, 40, 40);
  color: white;
}

.card img {
  max-width: 100%;
  height: 190px;
  margin: 0;
}

.card .card-text {
  padding: 0 5px;
}

.card-text h2 {
  font-weight: bold;
}

p {
  margin-bottom: 10px;
}
</style>
