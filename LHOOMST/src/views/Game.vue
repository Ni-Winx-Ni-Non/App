<script>
import Quizz from "../components/Quizz.vue"
import Captcha from "../components/Captcha.vue"
import Memo from "../components/Memo.vue"
import FourImagesOneWord from "../components/FourImagesOneWord.vue"
export default {
  components: {
    Quizz,
    Captcha,
    Memo,
    FourImagesOneWord
  },
  data() {
    return {
      larg: null,
      haut: null,
      quizzResult: [],
      memoResult: [],
      gameSelect: 0,
      quizSelect: false,
      memoSelect: false,
      imageSelect: false,
      captcha: true,
      indexGame: 0,
      cloud: [
        {x: 200, y: 1450, visible: false},
        {x: 840, y: 1400, visible: false},
        {x: 790, y: 1000, visible: false},
        {x: 550, y: 1260, visible: false},
        {x: 340, y: 960, visible: false},
        {x: 70, y: 1080, visible: false},
        {x: 200, y: 730, visible: false},
        {x: 650, y: 830, visible: false},
        {x: 755, y: 520, visible: false},
        {x: 55, y: 380, visible: false},
      ]
    }
  },
  methods: {
    emitQuizz(params) {
      console.log("Emit: " + JSON.stringify(params))
    },
    generate() {
      if (document.getElementById('view') != null) {
        this.larg = document.getElementById('view').clientWidth;
        this.haut = document.getElementById('view').clientHeight;
      }
    },
    nextGame() {
      this.cloud[this.indexGame].visible = false
      this.indexGame++
      if (this.gameSelect == 0) {
        this.imageSelect = true
        this.gameSelect++
      } else if (this.gameSelect == 1) {
        this.quizSelect = true
        this.gameSelect++
      } else {
        this.memoSelect = true
        this.gameSelect = 0
      }
    },
    nextGameEnd(params) {
        if (this.memoSelect) {
            this.memoSelect = false
            this.memoResult.push(params.result)
        }
        if (this.quizSelect) {
            this.quizSelect = false
            this.quizzResult.push(params.result)
        }
        if (this.imageSelect) {
            this.imageSelect = false
        }
        if (this.indexGame < this.cloud.length) {
            this.cloud[this.indexGame].visible = true
        } else {
            alert("Bravo !" )
            console.log("Show Result")
        }
    }
  },
  mounted() {
    this.cloud[this.indexGame].visible = true
    window.addEventListener('resize', () => {
      this.generate()
    });
    this.generate()
  }
}
</script>

<template>
  <div class="main">
    <div class="ratioView">
      <div id="view" class="view">
        <button @click="$router.back()" style="position: absolute; top: 20px; left: 20px" id="enter">Quitter</button>
        <div v-for="(item, index) in cloud" :key="index">
          <div @click="nextGame()" :style="'height: ' + (200 * haut) / 1920 + 'px; width: ' + (200 * larg) / 1080 + 'px; position: absolute; top: ' + (item.y * haut)/ 1920 + 'px; left:' + (item.x * larg) / 1080 + 'px'" style="border: 1px solid #252525; cursor: pointer" v-if="item.visible"></div>
        </div>
      </div>
    </div>
    <Quizz v-if="quizSelect" @endQuizz="nextGameEnd" />
    <Memo v-if="memoSelect" @endMemo="nextGameEnd" />
    <FourImagesOneWord v-if="imageSelect" @endGame="nextGameEnd"/>
    <div v-if="captcha" style="background-color: white; height: 100vh">
        <Captcha @EndCaptcha="captcha = false" />
    </div>
  </div>
</template>

<style scoped>
button {
    background-color: #3C7196;
    color: white;
    border: 2px solid #3C7196;
    padding: 0.85rem;
    border-radius: 1rem;
    font-size: 1.5rem;
    font-weight: bold;
    transition-duration: 0.4s;
}
#enter {
    margin-top: 1rem;
    margin-bottom: 2rem;
}
#info:hover,
#enter:hover {
    background-color: #CAF7F7;
    color: #3C7196;
    border: 2px solid #3C7196;
}
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
  background-image: url('../assets/back.png');
  background-size: cover;
  background-position: center;
}
</style>