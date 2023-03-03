<script>
export default {
  emits: ["on-selection"],
  props: {
    question: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      choosen: String,
    }
  },
}
</script>

<template>
  <div>
    <h3>{{ this.question.text }}</h3>
    <div v-for="choice in this.question.answers" :key="choice">
      <input
        type="radio"
        :value="choice"
        :id="choice"
        v-model="choosen"
        @on-change="$emit('on-selection', choosen)"
      />
      <label :for="choice">{{ choice }}</label>
    </div>
  </div>
</template>
