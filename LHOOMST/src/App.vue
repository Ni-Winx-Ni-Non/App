<script>
import Quizz from "./components/Quizz.vue"
import Home from "./components/Home.vue"
import Captcha from "./components/Captcha.vue"
export default {
  components: {
    Home
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
      <Home />
    </div> 
</template>