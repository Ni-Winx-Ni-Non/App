<script>
export default {
    methods: {
        scrolldown() {
            var el = document.getElementById('more_informations');
            el.scrollIntoView({ block: 'end', behavior: 'smooth' });
        },
        scrollup() {
            var el = document.getElementById('main_page');
            el.scrollIntoView({ block: 'end', behavior: 'smooth' });
        },
        enterGame() {
            this.$router.push('/game')
        }
    }
}
</script>

<template>
    <div style="width: 100vw; overflow-y: hidden; display: flex; justify-content: center">
        <div>
            <div id="main_page">
                <div id="title">
                    <h1>Bienvenue dans LHOOMST !</h1>
                </div>
                <div id="center">
                    <img id="logo" src="../assets/logoapp.png" style="width:20rem ;">
                    <div>
                        <button @click="enterGame()" id="enter">Entrer dans le jeu</button>
                    </div>
                </div>
                <div id="informations">
                    <button id="info" @click="scrolldown()">+ d'informations</button>
                </div>
            </div>

            <div id="more_informations">
                <div style="text-align: center;">
                    <button id="back_to_menu" @click="scrollup()">Revenir au menu</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#main_page {
    text-align: center;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
#logo {
    margin-left: auto;
    margin-right: auto;
}
#title {
    margin: 3rem 2rem 0 2rem;
    background-color: #FC9E8B;
    padding-top: 2rem;
    padding-bottom: 2rem;
    border-radius: 2rem;
}
h1 {
    color: #3C7196;
    font-weight: bold;
}
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
#back_to_menu:hover {
    background-color: #3C7196;
    color: white;
    border: 2px solid white;
}
#info {
    border-radius: 1rem 1rem 0rem 0rem;
    margin-bottom: 0;
    cursor: help;
    color: white;
    font-size: 1rem;
}
#back_to_menu {
    text-align: center;
    background-color: white;
    border-radius: 0rem 0rem 1rem 1rem;
    border: 2px solid white;
    color: #3C7196;
    font-size: 1rem;
}
#more_informations {
    height: 100vh;
    width: 100%;
    background-color: #3C7196;
}
</style>