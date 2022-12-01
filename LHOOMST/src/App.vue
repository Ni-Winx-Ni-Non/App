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
  <div class="main">
    <div class="ratioView">
      <div class="view">
        <Quizz @emitValid="emitQuizz" />
      </div>
    </div>
  </div>
</template>

<style>
body {
  overflow: hidden;
}
.main {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  position: relative;
}
.ratioView {
  position: absolute;
  margin: auto;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  max-width: 100%;
  max-height: 100%;
  aspect-ratio: 9/16;
}
.view {
  border: 1px solid #252525;
  aspect-ratio: 9/16;
  max-height: 100%;
}
</style>