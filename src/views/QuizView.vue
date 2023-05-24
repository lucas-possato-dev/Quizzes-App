<script setup>
import Question from "../components/Question.vue";
import Header from "../components/QuizHeader.vue";
import Result from "../components/Result.vue";
import quizes from "../data/quizes.json";
import { useRoute } from "vue-router";
import { ref, computed } from "vue";

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizes.find((q) => q.id === quizId);
const currentQuestionIndex = ref(0);
const correctAnswers = ref(0);
const showResults = ref(false);
const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    correctAnswers.value++;
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = true;
  }
  currentQuestionIndex.value++;
};

/*const questionStatus = ref(
  `${currentQuestionIndex.value}/${quiz.questions.length}`
);

watch(
  () => currentQuestionIndex.value,
  () => {
    questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`;
  }
);*/

const questionStatus = computed(() => {
  return `${currentQuestionIndex.value}/${quiz.questions.length}`;
});

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);
</script>

<template>
  <div>
    <Header :questionStatus="questionStatus" :barPercentage="barPercentage" />
    <div>
      <Question
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
      />
      <Result
        v-else
        :quizQuestionLength="quiz.questions.length"
        :correctAnswers="correctAnswers"
      />
    </div>
  </div>
</template>
