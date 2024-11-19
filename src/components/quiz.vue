<template>
  <div class="quiz-container">
    <form @submit.prevent="submitQuiz" class="quiz-form">
      <div v-for="question in quizQuestions" :key="question.id" class="question-block">
        <h2>{{ question.title }}</h2>
        <select v-model="question.userAnswer" required>
          <option value="" disabled>Select your answer</option>
          <option v-for="option in question.options" :key="option" :value="option">
            {{ option }}
          </option>
        </select>

        <p
          v-if="question.submitted"
          :class="{
            correct: question.isCorrect,
            incorrect: !question.isCorrect,
          }"
        >
          {{ question.feedback }}
        </p>
      </div>

      <button type="submit" :disabled="isSubmitted">Submit Answers</button>
    </form>

    <div v-if="isSubmitted" class="score-section">
      <h3>Your Score: {{ score }} / {{ quizQuestions.length }}</h3>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from "vue";

interface QuizQuestion {
  id: number;
  title: string;
  options: string[];
  correctAnswer: string;
  userAnswer: string;
  isCorrect: boolean;
  submitted: boolean;
  feedback: string;
}

const quizQuestions = reactive<QuizQuestion[]>([
  {
    id: 1,
    title: "What is the largest mammal in the world?",
    options: ["African Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
    correctAnswer: "Blue Whale",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 2,
    title: "Which bird is known for its impressive mimicry of human speech?",
    options: ["Eagle", "Penguin", "Parrot", "Sparrow"],
    correctAnswer: "Parrot",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 3,
    title: "What is the fastest land animal?",
    options: ["Cheetah", "Lion", "Gazelle", "Pronghorn Antelope"],
    correctAnswer: "Cheetah",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 4,
    title: 'Which animal is known as the "King of the Jungle"?',
    options: ["Tiger", "Elephant", "Lion", "Leopard"],
    correctAnswer: "Lion",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 5,
    title: "What is the primary diet of a giant panda?",
    options: ["Bamboo", "Fish", "Insects", "Fruits"],
    correctAnswer: "Bamboo",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 6,
    title: "Which marine animal has three hearts?",
    options: ["Dolphin", "Octopus", "Shark", "Sea Turtle"],
    correctAnswer: "Octopus",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 7,
    title: "What is the tallest animal in the world?",
    options: ["Elephant", "Giraffe", "Kangaroo", "Ostrich"],
    correctAnswer: "Giraffe",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 8,
    title: "Which reptile is known for its ability to change colors?",
    options: ["Crocodile", "Chameleon", "Iguana", "Gecko"],
    correctAnswer: "Chameleon",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 9,
    title: "What is the only mammal capable of true flight?",
    options: ["Bat", "Flying Squirrel", "Sugar Glider", "Colugo"],
    correctAnswer: "Bat",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
  {
    id: 10,
    title: "Which insect is known for its complex social structure and ability to build intricate colonies?",
    options: ["Butterfly", "Dragonfly", "Ant", "Beetle"],
    correctAnswer: "Ant",
    userAnswer: "",
    isCorrect: false,
    submitted: false,
    feedback: "",
  },
]);

const isSubmitted = ref(false);
const score = ref(0);

const submitQuiz = () => {
  score.value = 0;

  quizQuestions.forEach((question) => {
    question.submitted = true;
    if (question.userAnswer === question.correctAnswer) {
      question.isCorrect = true;
      question.feedback = "Correct!";
      score.value += 1;
    } else {
      question.isCorrect = false;
      question.feedback = `Incorrect. The correct answer is "${question.correctAnswer}".`;
    }
  });

  isSubmitted.value = true;
};
</script>

<style scoped>
.quiz-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

.logo {
  border-radius: 10px;
}

main {
  text-align: center;
  margin-bottom: 30px;
}

.quiz-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.question-block {
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.question-block h2 {
  margin-bottom: 10px;
}

.question-block select {
  width: 100%;
  padding: 8px;
  font-size: 16px;
}

.question-block p {
  margin-top: 10px;
  font-weight: bold;
}

.correct {
  color: green;
}

.incorrect {
  color: red;
}

button {
  padding: 10px 20px;
  font-size: 18px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:disabled {
  background-color: #a5d6a7;
  cursor: not-allowed;
}

.score-section {
  text-align: center;
  margin-top: 30px;
}
</style>
