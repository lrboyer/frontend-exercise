<template>
  <form @submit.prevent="handleSubmit">
    <template v-if="!summary">
      <Question
        :question="currentQuestion"
        :questionIndex="currentIndex"
        :onSubmit="handleQuestionSubmit"
      />
    </template>

    <template v-else>
      <p>{{ responses }}</p>
    </template>
  </form>
</template>

<script>
import Question from "./components/Question.vue";

export default {
  components: {
    Question
  },
  props: {
    questions: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      currentIndex: 0,
      responses: [],
      summary: 0
    };
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentIndex];
    }
  },
  methods: {
    showSummary() {
      this.summary = 1;
    },
    handleQuestionSubmit(answer) {
      let response = {
        "questionNum": this.currentIndex,
        "question": this.currentQuestion.text,
        "response": answer
      };

      this.responses.push(response);

      if (this.currentIndex != this.questions.length - 1) {
        this.currentIndex += 1;
      } else {
        this.showSummary();
      }
    },
    handleSubmit() {
      // Handle form submission (if needed)
    }
  }
};
</script>
