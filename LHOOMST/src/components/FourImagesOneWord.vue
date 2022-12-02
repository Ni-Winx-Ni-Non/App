<script>

export default {

    data() {
        return {
            images: {
                1: "https://play-lh.googleusercontent.com/kEeTu6YanMhv1eaCEKddk75jRFtclLrPeeDZ4G0UnpOxkcuspVs_2WXVxCwpVgPulf-O",
                2: "https://play-lh.googleusercontent.com/kEeTu6YanMhv1eaCEKddk75jRFtclLrPeeDZ4G0UnpOxkcuspVs_2WXVxCwpVgPulf-O",
                3: "https://play-lh.googleusercontent.com/kEeTu6YanMhv1eaCEKddk75jRFtclLrPeeDZ4G0UnpOxkcuspVs_2WXVxCwpVgPulf-O",
                4: "https://play-lh.googleusercontent.com/kEeTu6YanMhv1eaCEKddk75jRFtclLrPeeDZ4G0UnpOxkcuspVs_2WXVxCwpVgPulf-O"
            },
            fullsizeImage: undefined,

            word: [undefined, undefined, undefined, '-', undefined, undefined, undefined],

            letters: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R']
        }
    },

    methods: {
        onImageClick(id) {
            this.fullsizeImage = id;
        },

        onImageContainerClick() {
            this.fullsizeImage = undefined;
        },

        onLetterClick(letter) {
            if (this.isLetterInWord(letter)) {
                return;
            }

            for (let i = 0; i < this.word.length; i++) {
                if (!this.word[i]) {
                    this.word[i] = letter;
                    if (this.isFinished()) {
                        this.verifyWord();
                    }
                    return;
                }
            }
        },

        onLetterRemove(index) {
            this.word[index] = undefined;
        },

        isLetterInWord(letter) {
            for (let i = 0; i < this.word.length; i++) {
                if (this.word[i] === letter) {
                    return true;
                }
            }

            return false;
        },

        isFinished() {
            for (let i = 0; i < this.word.length; i++) {
                if (this.word[i] === undefined) {
                    return false;
                }
            }

            return true;
        },

        verifyWord() {
            const elem = document.getElementById('word');
            elem.classList.add('shaking');
            setTimeout(() => elem.classList.remove('shaking'), 750);
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
            <div v-for="letter, index in word" class="letter-hole" :class="{ letter: letter && letter !== ' ' && letter !== '-', hole: !letter, delimiter: letter === ' ' || letter === '-' }" @click="onLetterRemove(index)">
                {{ letter ?? '' }}
            </div>
        </div>

        <div id="letters" class="panel letter-hole-container">
            <div v-for="letter in letters" class="letter-hole" :class="{ letter: !isLetterInWord(letter), hole: isLetterInWord(letter) }" @click="onLetterClick(letter)">
                {{ isLetterInWord(letter) ? '' : letter }}
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
        transition: transform 0.1s ease;
    }

    .image-thumbnail:hover {
        transform: scale(105%);
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