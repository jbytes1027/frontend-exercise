<script>
export default {
  emits: ["on-restart"],
  props: {
    answers: {
      type: Array,
    },
  },
}
</script>

<template>
  <div id="summary">
    <h1>Summary</h1>
    <div v-for="answer in answers" :key="answer.question">
      <h3>{{ answer.question }}</h3>
      <p>{{ answer.response }}</p>
    </div>
    <button @click="$emit('on-restart')">Restart</button>
    <br />
  </div>
</template>
