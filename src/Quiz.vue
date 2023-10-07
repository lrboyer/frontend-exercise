<template>
  <div id="focus">
    <form @submit.prevent="handleSubmit">
      <template v-if="!summary">
        <Question :question="currentQuestion" :questionIndex="currentIndex" :onSubmit="handleQuestionSubmit" />
      </template>

      <template v-else>
        <Summary :summary="responses" />
      </template>
    </form>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Summary from "./components/Summary.vue";

export default {
  components: {
    Question,
    Summary
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
        this.handleSubmit()
      }
    },
    handleSubmit() { //incase more logic is needed
      this.showSummary();
    }
  }
};
</script>

<style>
body {
  font-family: Arial;
  background-color: #2b2b2b;
  margin: 0;
  padding: 0;
}

form {
  max-width: 600px;
  margin: 0 auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3);
}

#focus {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

button[type="submit"] {
  background-color: #007bff;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

button[type="submit"]:hover {
  background-color: #0050a5;
}
</style>