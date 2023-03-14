<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} / {{ questions.length }} 题
      </div>
    </div>
    <tansition-group name="fade">
      <div
        class="single-question"
        v-for="(question, index) in questions"
        :key="question.q"
        v-show="index === questionsAnswered"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </tansition-group>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: ["questions", "questionsAnswered"],
  emits: ["question-answered"],
  methods: {
    selectAnswer(isCorrect) {
      // 因为想要在App.vue中跟踪正确答案，以便将正确答案的数量传递给Result组件
      this.$emit("question-answered", isCorrect);
    },
  },
};
</script>

<style></style>
