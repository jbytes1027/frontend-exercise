<script>
import QuestionPrompt from "./QuestionPrompt.vue"
import Summary from "./Summary.vue"

export default {
  components: {
    QuestionPrompt,
    Summary,
  },
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  setup() {
    return {
      STATES: {
        Start: 0,
        Ask: 1,
        Summary: 2,
      },
    }
  },
  data() {
    return {
      currQuestionIndex: 0,
      answers: [],
      state: this.STATES.Start,
    }
  },
  methods: {
    onStart() {
      this.answers = []
      this.currQuestionIndex = 0
      this.state = this.STATES.Ask
    },
    onQuestionAnswered(answer) {
      this.answers.push(answer)

      // if not last question
      if (this.currQuestionIndex + 1 !== this.questions.length)
        this.currQuestionIndex++
      else this.state = this.STATES.Summary
    },
    onRestart() {
      this.state = this.STATES.Start
    },
  },
}
</script>

<template>
  <div id="quiz">
    <div id="start" v-if="state === STATES.Start">
      <h1>Quiz</h1>
      <p>Please answer a couple questions</p>
      <button @click="onStart">Begin</button>
    </div>
    <QuestionPrompt
      v-if="state === STATES.Ask"
      :question="questions[currQuestionIndex]"
      @on-answer="onQuestionAnswered"
    />
    <Summary
      v-if="state === STATES.Summary"
      :answers="answers"
      @on-restart="onRestart"
    />
  </div>
</template>
