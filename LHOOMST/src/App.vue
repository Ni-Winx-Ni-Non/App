<script>
import Quizz from "./components/Quizz.vue"
export default {
  components: {
    Quizz
  },
  methods: {
    emitQuizz(params) {
      console.log("Emit: " + JSON.stringify(params))
    }
  }
}
</script>

<template>
    <div>
      <Quizz @emitValid="emitQuizz" />
    </div>
</template>