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
        }
    }
}

</script>

<template>
    <div id="main_page">
        <div id="title">
            <h1>Bienvenue dans LHOOMST !</h1>
        </div>
        <div id="center">
            <img id="logo" src="../assets/logoapp.png" style="width:20rem ;">
            <div>
                <button @click="$router.push('/game')" id="enter">Entrer dans le jeu</button>
            </div>
        </div>
        <div id="informations">
            <button id="info" @click="scrolldown()">+ d'informations</button>
        </div>
    </div>

    <div id="more_informations">
        <div style="text-align: center;">
            <button id="back_to_menu" @click="scrollup()">Revenir au menu</button>
            <div class="explications">
                <h2 style="font-weight: bold; margin-bottom: 1rem;">Bienvenue dans LHOOMST !</h2>

                <h3>Le jeu qui informe sur la santé sexuelle : peu importe ton âge ou ton sexe, ce jeu t’apprendra ou te
                    rafraîchira la mémoire en te donnant des informations sur les IST et la contraception 😉</h3>

                <h3>Viens découvrir ce monde à travers les différents niveaux qui te sont proposés.</h3>

                <h3>Bonne aventure à toi !</h3>
                <div id="bottom">
                    <img id="ballon" src="../assets/ballon.png">
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
    margin-bottom: 3rem;
}

#more_informations {
    height: 100vh;
    width: 100%;
    background-color: #3C7196;
}

.explications {
    margin: 2rem;
    text-align: justify;
    text-align-last: left;
    color: white;
}

#bottom {
    width : 70vw;
    margin: auto;
    margin-top: 1rem;
    padding: 1rem;
    border-radius: 1rem;
    text-align: center;
}

#ballon{
    display: block;
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    border-radius: 1rem;
    margin-bottom: 1rem;
}

</style>