<script>
export default {
  emits: ["on-answer"],
  props: {
    question: {
      type: Object,
      required: true,
    },
  },
  methods: {
    onAnswer() {
      let answer = {
        question: this.question.text,
        response: this.choosen,
      }

      this.$emit("on-answer", answer)
      this.choosen = undefined
    },
  },
  data() {
    return {
      choosen: undefined,
    }
  },
}
</script>

<template>
  <div>
    <h3>{{ this.question.text }}</h3>
    <div v-for="choice in this.question.answers" :key="choice">
      <input type="radio" :value="choice" :id="choice" v-model="choosen" />
      <label :for="choice">{{ choice }}</label>
    </div>
    <br />
    <button :disabled="!choosen" @click="onAnswer">Next</button>
  </div>
</template>
