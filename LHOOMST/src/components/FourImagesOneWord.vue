<script>

import json from '../assets/json/four_images_one_word.json';
const instance = json[Math.floor(Math.random() * json.length)];
instance.word = instance.word.toUpperCase();

export default {
    data() {
        return {
            images: {
                1: "https://controller.genesis-mc.fr/ndi/" + instance.hints[0] + ".png",
                2: "https://controller.genesis-mc.fr/ndi/" + instance.hints[1] + ".png",
                3: "https://controller.genesis-mc.fr/ndi/" + instance.hints[2] + ".png",
                4: "https://controller.genesis-mc.fr/ndi/" + instance.hints[3] + ".png"
            },
            fullsizeImage: undefined,

            userWord: this.initWord(),

            letters: this.initLetters()
        }
    },

    methods: {
        initWord() {
            const emptyWord = [];
            for (let i = 0; i < instance.word.length; i++) {
                emptyWord.push(undefined);
            }
            console.log(emptyWord);
            return emptyWord;
        },

        initLetters() {
            const letters = [];
            for (let i = 0; i < instance.word.length; i++) {
                letters.push({ index: undefined, letter: instance.word.charAt(i) });
            }
            letters.sort(() => Math.random() - 0.5);
            for (let i = 0; i < letters.length; i++) {
                letters[i].index = i;
            }
            console.log(letters);
            return letters;
        },


        onImageClick(id) {
            this.fullsizeImage = id;
        },

        onImageContainerClick() {
            this.fullsizeImage = undefined;
        },

        onLetterClick(letter) {
            if (!letter || this.isLetterPlaced(letter)) {
                return;
            }

            for (let i = 0; i < this.userWord.length; i++) {
                if (!this.userWord[i]) {
                    this.letters[letter.index] = undefined;
                    this.userWord[i] = letter;

                    if (this.isFinished()) {
                        this.verifyWord();
                    }
                    return;
                }
            }
        },

        onLetterRemove(letter) {
            if (!letter || letter.letter === ' ' || letter.letter === '-') {
                return;
            }
            let i;
            for (i = 0; i < this.userWord.length; i++) {
                if (this.userWord[i] && this.userWord[i].index === letter.index) {
                    break;
                }
            }
            if (i === this.userWord.length) {
                return;
            }
            this.userWord[i] = undefined;
            this.letters[letter.index] = letter;
        },

        isLetterPlaced(letter) {
            for (let i = 0; i < this.userWord.length; i++) {
                if (this.userWord[i] && this.userWord[i].index === letter.index) {
                    return true;
                }
            }

            return false;
        },

        isFinished() {
            for (let i = 0; i < this.userWord.length; i++) {
                if (this.userWord[i] === undefined) {
                    return false;
                }
            }

            return true;
        },

        isDone() {
            let result = '';
            this.userWord.forEach(letter => result += letter.letter);
            return result === instance.word;
        },

        verifyWord() {
            if (this.isDone()) {
                this.$emit('endGame')
            } else {
                const elem = document.getElementById('word');
                elem.classList.add('shaking');
                setTimeout(() => elem.classList.remove('shaking'), 750);
            }
        }
    }

}

</script>





<template>

    <div id="container">
        <div id="images" class="panel" @click="onImageContainerClick()">
            <img class="image-thumbnail" id="image-1" @click.stop="onImageClick(1)" :src="images[1]" alt="Image 1" />
            <img class="image-thumbnail" id="image-2" @click.stop="onImageClick(2)" :src="images[2]" alt="Image 2" />
            <img class="image-thumbnail" id="image-3" @click.stop="onImageClick(3)" :src="images[3]" alt="Image 3" />
            <img class="image-thumbnail" id="image-4" @click.stop="onImageClick(4)" :src="images[4]" alt="Image 4" />
            <Transition>
                <img v-if="fullsizeImage" id="image-fullsize" :src="images[fullsizeImage]" alt="Image plein écran" />
            </Transition>
        </div>

        <div id="word" class="panel letter-hole-container">
            <div v-for="letter in userWord" class="letter-hole" :class="{ letter: letter && letter.letter !== ' ' && letter.letter !== '-', hole: !letter, delimiter: letter && (letter.letter === ' ' || letter.letter === '-') }" @click="onLetterRemove(letter)">
                {{ letter ? letter.letter : '' }}
            </div>
        </div>

        <div id="letters" class="panel letter-hole-container">
            <div v-for="letter in letters" class="letter-hole" :class="{ letter: letter, hole: !letter }" @click="onLetterClick(letter)">
                {{ letter ? letter.letter : '' }}
            </div>
        </div>
    </div>

</template>





<style scoped>

    #container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }



    .panel {
        background-color: #FC9E8B;
        border-radius: 2rem;
        box-shadow: 0 1rem 3rem inset, 0 0.5rem 2rem black;
        padding: 1.5rem;
    }



    #images {
        display: grid;
        grid-gap: 1rem;
        margin-bottom: 0.5rem;
    }

    img {
        cursor: pointer;
    }


    .image-thumbnail {
        width: 7.5rem;
        border-radius: 1.40625rem;
        box-shadow: 0 0 0.5rem black;
        transition: 0.1s ease;
    }

    .image-thumbnail:hover {
        transform: scale(105%);
        box-shadow: 0 0 0.65rem black;
    }

    #image-1 {
        grid-column: 1;
        grid-row: 1;
    }

    #image-2 {
        grid-column: 2;
        grid-row: 1;
    }

    #image-3 {
        grid-column: 1;
        grid-row: 2;
    }

    #image-4 {
        grid-column: 2;
        grid-row: 2;
    }


    #image-fullsize {
        position: absolute;
        z-index: 1;
        width: 18rem;
        top: 0.5rem;
        left: 0.5rem;
        border-radius: 3.375rem;
        box-shadow: 0 0 1rem black;
    }

    .v-enter-active,
    .v-leave-active {
        transition: opacity 0.5s ease;
    }

    .v-enter-from,
    .v-leave-to {
        opacity: 0;
    }



    .letter-hole-container {
        display: grid;
        grid-gap: 0.2rem;
        grid-template-columns: repeat(6, 1fr);
    }

    .letter-hole {
        width: 2.5rem;
        height: 2.5rem;
        border-radius: 0.5rem;
    }



    #word {
        margin-bottom: 0.5rem;
    }

    .hole {
        background-color: #202020;
        box-shadow: 0 0.15rem 0.2rem black inset;
    }



    .letter {
        background-color: white;
        box-shadow: 0 0.15rem 0.2rem black;
        text-align: center;
        color: black;
        font-size: 1.55rem;
        font-weight: bold;
        cursor: pointer;
        transition: background-color 0.2s ease;
    }

    .letter:hover {
        background-color: #E0E0E0;
    }



    .delimiter {
        text-align: center;
        color: black;
        font-size: 1.55rem;
        font-weight: bold;
    }



    @keyframes shake {
    0%   {transform: translateX(0%);}
    10%   {transform: translateX(0.25rem);}
    20%   {transform: translateX(-0.25rem);}
    30%   {transform: translateX(0.25rem);}
    40%   {transform: translateX(-0.25rem);}
    50%   {transform: translateX(0.25rem);}
    60%   {transform: translateX(-0.25rem);}
    70%   {transform: translateX(0.25rem);}
    80%   {transform: translateX(-0.25rem);}
    90%   {transform: translateX(0.25rem);}
    100%   {transform: translateX(0%);}
}

    .shaking {
        animation-name: shake;
        animation-duration: 0.75s;
    }

</style>