<script>
export default {
    data() {
        return {
            questions: [
                { id: 1, description: "Si je ne vais pas jusqu’à la pénétration, il est impossible que j’attrape une IST.", response: false, explication:"Certaines IST peuvent être « manuportées », c’est-à-dire transmises par le biais des mains, quand il y a échange ou contact de fluides (sécrétions vaginales ou sperme)." },
                { id: 2, description: "Si mon test VIH est négatif, je suis aussi négatif aux autres IST.", response: false , explication:"Le test VIH ne dépiste pas les autres IST !"},
                { id: 3, description: "Si mon test VIH est négatif, je suis aussi négatif aux autres IST.", response: false , explication:"Le test VIH ne dépiste pas les autres IST !"},
                { id: 4, description: "Si mon test VIH est négatif, je suis aussi négatif aux autres IST.", response: false , explication:"Le test VIH ne dépiste pas les autres IST !"},
                { id: 5, description: "Si mon test VIH est négatif, je suis aussi négatif aux autres IST.", response: false , explication:"Le test VIH ne dépiste pas les autres IST !"},
            ],
            questionId: 0,
            correctAnswers: 0,
            questionAnswered: false,
            wellAnswered:false,
            gameOver:false
        }
    },
    methods: {
        questionSuivante() {
            this.questionAnswered = false
            this.questionId++
        },
        valid(id) {
            console.log("Question id: " + id)
            this.$emit('emitValid', { index: id })
        },
        answer(bool) {
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
        end(){
            this.gameOver =true;
        }
    }
}
</script>

<template>
    <div>

        <!-- Questions: on affiche une div pour chaque question -->
        <div v-if="!gameOver">
            <h1>Question {{( questionId +1)}} / 5</h1>
            <h2>{{ questions[questionId].description }}</h2>

            
            <div v-if="!questionAnswered" class="boutons">
                <button class="vrai-faux" @click="answer(true)">Vrai</button>
                <button class="vrai-faux" @click="answer(false)">Faux</button>
            </div>

            <div v-else>
                <h1 v-if="this.wellAnswered"> Bonne réponse !</h1>
                <h1 v-else style="color:red"> Mauvaise réponse :(</h1>
                <h2>{{ questions[questionId].explication }}</h2>

                <button v-if="(questionId < questions.length -1)" @click="questionSuivante">Suivant</button>
                <button v-else @click="end">Voir le score</button>

            </div>


        </div>

        <div v-else>
            <h1>Vous avez obtenu un score de {{this.correctAnswers}} / 5</h1>
        </div>

    </div>
</template>

<style scoped>


h1 {
 margin : 2rem;
}


button {
    background-color: #3C7196;
    color: white;
    border: 2px solid #3C7196;
    padding: 0.85rem;
    border-radius: 1rem;
    margin-bottom: 2rem;
    font-weight: bold;
    transition-duration: 0.4s;
}

button:hover {
    background-color: #CAF7F7;
    color: #3C7196;
    border: 2px solid #3C7196
}



button.vrai-faux {
    background-color: #3C7196;

}

.boutons {
    display: flex;
    justify-content: space-around;
}
</style>
