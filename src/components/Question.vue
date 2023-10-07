<template>
  <form @submit.prevent="submitAnswer">
    <div>
      <h1>{{ questionIndex + 1 }}. {{ question.text }}</h1>
      <div class="choices" v-for="(answer, index) in question.answers" :key="index">
        <input type="radio" :name="questionIndex" :value="answer" v-model="selectedAnswer" required />
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

<style scoped>
.choices {
  display: flex;
  align-items: center;
  margin: 10px;
}

.choices:first-child {
  margin-top: 0;
}

label {
  padding: 10px;
  padding-bottom: 7px;
}

</style>