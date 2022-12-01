<script>
export default {
    data() {
        return {
            title: 'Mon questionnaire',
            questions: [
                {
                    text: "Question 1",
                    responses: [
                        { text: 'Mauvaise réponse, dommage.' },
                        { text: 'Bonne réponse !', correct: true },
                    ]
                }, {
                    text: "Question 2",
                    responses: [
                        { text: 'Bonne réponse', correct: true },
                        { text: 'Mauvaise réponse' },
                    ]
                }
            ]
        }
    }
}
</script>

<template>
    <div>Quizz</div>
    <div>
      <!-- Titre du quiz -->
      <h1>{{ title }}</h1>
      <!-- Questions: on affiche une div pour chaque question -->
      <div v-for="question in questions">
        <h2>{{ question.text }}</h2>
        <!-- Responses: on affiche une balise li pour chaque réponse possible -->
        <ol>
          <li v-for="response in question.responses">
            <label>
              <input type="radio"> {{response.text}}
            </label>
          </li>
        </ol>
      </div>
    </div>
</template>

<style scoped>

</style>