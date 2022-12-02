<script>
export default {
    data() {
        return {
            captcha: null,
            inputField: "",
            statusTxt: null,
            allWords: ["Chlamydia", "Condylome", "Gardnerella vaginalis", "Gonorrhee", "Herpes", "Morpions", "Papillomavirus", "Sida", "Syphilis", "VIH", "Trichomonase", "Ureaplasma", "Uretrite"],
            
        }
    },

    methods: {
        getCaptcha() {
            let chosenWord = this.allWords[Math.floor(Math.random() * this.allWords.length)];
            this.captcha = chosenWord;
        },
        removeContent() {
            this.inputField = "";
            this.captcha = "";
            this.statusTxt = null;
        },
        checkCaptcha() {
            let inputVal = this.inputField;
            if(inputVal == this.captcha){ //if captcha matched
                //statusTxt.style.color = "#4db2ec";
                this.statusTxt = "Super ! Tu n'as pas l'air d'être un robot.";
                setTimeout(()=>{ //calling removeContent & getCaptcha after 2 seconds
                    this.$emit('EndCaptcha')
                }, 2000);
            }else{
                //statusTxt.style.color = "#ff0000";
                this.statusTxt = "Le captcha ne correspond pas.\nEssaie encore!";
                setTimeout(()=>{ //calling removeContent & getCaptcha after 2 seconds
                    this.removeContent();
                    this.getCaptcha();
                }, 2000);
            }
        }
    },
    mounted() {
        this.getCaptcha()
    }
}
</script>

<template>
    <div class="captcha_container">
        <h2>Captcha : Nom d'IST</h2>
        <div class="captcha-area">
            <div class="img_container">
                <img class="captcha_img" src="../assets/Background-captcha.png" alt="captcha">
                <span class="capt-text" style="color: white">{{ captcha }}</span>
            </div>
            <button @click="removeContent(); getCaptcha()" class="reload-button">Regénérer le captcha<i class="redo"></i></button>
        </div>
        <input @keyup.enter="checkCaptcha()" class="input_text" type="text" v-model="inputField" placeholder="Entrer le captcha">
            <button @click="checkCaptcha()" class="check-button">OK</button>
        <div class="status-txt">{{ statusTxt }}</div>
    </div>
</template>

<style scoped>

h2{
    text-align: center;
    margin-bottom: 0.5rem;
    color: white;
    font-weight: bold;
}

.captcha_container{
    width : 90vW;
    background-color: #8DB0C9;
    margin: auto;
    margin-top: 10rem;
    padding: 1rem;
    border-radius: 1rem;
    text-align: center;
}

.captcha_img{
    display: block;
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    border-radius: 1rem;
    margin-bottom: 1rem;
}

.capt-text{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 2.5rem;
    color: #555555;

    -webkit-user-select: none; /* Safari */
  -ms-user-select: none; /* IE 10 and IE 11 */
  user-select: none; /* Standard syntax */
}

button{
    background-color: #3C7196;
    color: white;
    border: 2px solid #3C7196;
    padding: 0.6rem;
    border-radius: 1rem;
    font-size: 0.8rem;
    font-weight: bold;
    transition-duration: 0.4s;
    margin-bottom: 1rem;
}

.check-button{
    padding: 0.3rem;
}

.input_text{
    border-radius: 0.3rem;
    margin-right: 0.5rem;
    border: 2px solid #3C7196;
    height: 1.7rem;
}

</style>