<template>
    <div class="summary">
        <h1>Quiz Summary</h1>
        <div class="questions">
            <div class="question" v-for="(response, index) in summary" :key="index">
                <strong>{{ response.questionNum + 1 }}. {{ response.question }}</strong>
                <p>You answered: {{ response.response }}</p>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    props: {
        summary: {
            type: Array,
            required: true
        }
    }
};
</script>
  
<style scoped>
.summary {
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3);
}

.questions {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.question {
    border-radius: 5px;
    padding: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

</style>
  