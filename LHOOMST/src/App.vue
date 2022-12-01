<script>
import FourImagesOneWord from "./components/FourImagesOneWord.vue"
export default {
  components: {
    FourImagesOneWord
  },
  methods: {
    emitQuizz(params) {
      console.log("Emit: " + JSON.stringify(params))
    }
  }
}
</script>

<template>
  <div id="main-container">
    <FourImagesOneWord id="four-images-one-word" />
  </div>
</template>

<style scoped>
  #main-container {
    width: 56.25vh;
    height: 100vh;
    transform: translateX(50%);
    border: solid red 1px;
  }

  #four-images-one-word {
  }
</style>