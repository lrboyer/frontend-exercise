<template>
  <form @submit.prevent="submitAnswer">
    <div>
      <h1>{{ questionIndex + 1 }}. {{ question.text }}</h1>
      <div v-for="(answer, index) in question.answers" :key="index">
        <input
          type="radio"
          :name="questionIndex"
          :value="answer"
          v-model="selectedAnswer"
          required
        />
        <label>{{ answer }}</label>
      </div>
      <button type="submit">Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    question: {
      type: Object,
      required: true
    },
    questionIndex: {
      type: Number,
      required: true
    },
    onSubmit: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      selectedAnswer: "",
    };
  },
  methods: {
    submitAnswer() {
      if (!this.selectedAnswer) {
        return;
      }
      this.onSubmit(this.selectedAnswer);
      this.selectedAnswer = "";
    }
  }
};
</script>
