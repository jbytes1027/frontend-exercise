<script>
import Question from "./Question.vue"

export default {
  components: {
    Question,
  },
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currQuestionIndex: 0,
      currChoice: String,
      answers: [],
      doneAsking: false,
    }
  },
  methods: {
    onNext() {
      let currQuestion = this.questions[this.currQuestionIndex]
      let answer = {
        question: currQuestion.text,
        response: this.currChoice,
      }
      this.answers.push(answer)

      // if not last question
      if (this.currQuestionIndex + 1 != this.questions.length)
        this.currQuestionIndex++
      else this.doneAsking = true
    },
  },
}
</script>

<template>
  <div id="quiz">
    <Question
      :question="questions[currQuestionIndex]"
      @on-selection="(choice) => (currChoice = choice)"
    />
    <br />
    <button type="button" @click="onNext">Next</button>
  </div>
</template>
