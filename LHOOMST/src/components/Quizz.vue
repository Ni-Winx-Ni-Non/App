<script>
import questionList from "../assets/questions-quiz.json"

export default {
    props: ['gameIndex'],
    data() {
        return {
            questions: questionList,
            questionId: -1,
            correctAnswers: 0,
            questionAnswered: false,
            wellAnswered: true,
            gameOver: false,
            game: -1
        }
    },
    methods: {
        init() {
            this.game = this.gameIndex,
                this.questionId = (this.game - 1) * 5
        },
        questionSuivante() {
            this.wellAnswered = true
            this.questionAnswered = false
            this.questionId++
        },
        valid() {
            console.log("Question id: " + this.questionId)
            this.$emit('emitValid', { index: this.questionId })
        },
        answer(bool) {
            console.log(this.questionAnswered)
            if (this.questions[this.questionId].response == bool) {
                this.wellAnswered = true
                console.log('Win')
                this.correctAnswers++

                console.log(this.correctAnswers)
            } else {
                this.wellAnswered = false
                console.log('Lose')
            }
            this.questionAnswered = true
        },
        end() {
            this.gameOver = true;
        },
        reset() {

            //this.questionId = 0,
            this.correctAnswers = 0,
                this.questionAnswered = false,
                this.wellAnswered = true,
                this.gameOver = false,
                this.game++,
                console.log('Quizz destroyed'),
                console.log(this.questionId)

        }

    }
}

</script>

<template>
    <div v-if="(questionId == -1)" class="playing">
        <div class="card">
            <div class="content">
                <h2>Quiz :<br />5 questions de savoir sur la sexualité.</h2>
            </div>

        </div>
        <div class="boutons">
            <button @click="init()">Démarrer le quiz !</button>
        </div>
    </div>
    <div v-else-if="!gameOver" class="playing" :class="this.wellAnswered ? '' : 'wrong'">
        <div class="card">
            <h1 style="margin-bottom: 0px">Question {{ (questionId + 1 -((this.game-1)*5)) }} / 5</h1>

            <div v-if="questionAnswered" class="content">
                <div>
                    <h1 style="margin-top: 0px" v-if="this.wellAnswered"> Bonne réponse !</h1>
                    <h1 v-else style="color:red; margin-top: 0px"> Mauvaise réponse :(</h1>
                    <h2>{{ questions[questionId].explication }}</h2>
                </div>
            </div>
            <div class="content" v-else>
                <h2>{{ questions[questionId].description }}</h2>
            </div>
        </div>

        <div v-if="!questionAnswered" class="boutons">
            <button @click="answer(true)">Vrai</button>
            <button @click="answer(false)">Faux</button>
        </div>

        <div v-else class="boutons">
            <button v-if="(questionId < game * 5 - 1)" @click="questionSuivante">Suivant</button>
            <button v-else @click="end">Voir le score</button>
        </div>


    </div>

    <div v-else class="score">
        <h1>Vous avez obtenu un score de {{ this.correctAnswers }} / 5</h1>
        <div class="boutons">
            <button @click="($emit('endQuizz', { result: correctAnswers }), reset())">Continuer</button>
        </div>

    </div>

</template>

<style scoped>
h1 {
    margin: 2rem;
    text-align: center;
}

.score {
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100%;
    background-color: white;
}

button {
    background-color: #3C7196;
    color: white;
    border: 2px solid #3C7196;
    padding: 2vh 8vh;
    border-radius: 2rem;
    margin-top: 2rem;
    margin-bottom: 2rem;
    font-size: 1rem;
    font-weight: bold;
    transition: 0.3s ease;
}

button:hover {
    background-color: #CAF7F7;
    color: #3C7196;
    border: 2px solid #3C7196
}


.boutons {
    display: flex;
    justify-content: space-around;

}

.card {
    background-color: white;
    box-shadow: 0.3rem 0.2rem 0.5rem 0rem rgba(0, 0, 0, 0.4);
    border-radius: 1rem;
    height: 40rem;
    margin: 1rem;
    margin-top: 0;
    padding: 2rem;
    padding-bottom: 6rem;
    text-align: center;

}

.playing {
    background-color: #8DB0C9;
    height: 100%;
    width: 100%;
    padding-top: 3rem;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    transition: 0.3s ease;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

}

.wrong {
    background-color: #FC9E8B;
}

.content {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
}
</style>