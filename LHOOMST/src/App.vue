<script>
import Quizz from "./components/Quizz.vue"
import Memo from "./components/Memo.vue"
export default {
  components: {
    Quizz,
    Memo
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
      <Memo  />
    </div>
</template>