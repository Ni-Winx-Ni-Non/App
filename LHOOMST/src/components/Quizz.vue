<script>
export default {
    data() {
        return {
            questions: [
        }
    },
    methods: {
        valid(id) {
            console.log("Question id: " + id)
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
