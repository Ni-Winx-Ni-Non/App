<script>
export default {
    data() {
        return {
            questions: [
                {id: 1, title: 'MST', description: "Qu'est ce que c'est ?"},
                {id: 2, title: 'IST', description: "Qu'est ce que c'est ?"},
                {id: 2, title: 'IST', description: "Qu'est ce que c'est ?"},
                {id: 2, title: 'IST', description: "Qu'est ce que c'est ?"},
                {id: 2, title: 'IST', description: "Qu'est ce que c'est ?"},
                {id: 2, title: 'IST', description: "Qu'est ce que c'est ?"},
            ]
        }
    },
    methods: {
        valid(id) {
            console.log("Question id: " + id)
            this.$emit('emitValid', {index: id})
        }
    }
}
</script>

<template>
    <div class="grid4">
        <div v-for="(item, index) in questions" :key="index">
            <h2>{{ item.title }}</h2>
            <p>{{ item.description }}</p>
            <button @click="valid(index)">Valider</button>
        </div>
    </div>
</template>

<style>
.grid4 {
    display: grid;
    box-sizing: border-box;
    gap: 1rem;
    grid-template-columns: repeat(4, minmax(0, 1fr));
}
</style>