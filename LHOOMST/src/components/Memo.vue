<script>
export default {
    data() {
        return {
          coups: 0,
      temps: 0,           
            cartes: [
                {id: 1, Nom: 'Chlamydia', texte: "Chlamydia", visible: 0, typecarte:true, idcomplementaire: 9},
                {id: 2, Nom: 'Condylome', texte: "Condylome", visible: true, typecarte:true, idcomplementaire: 10},
                {id: 3, Nom: 'trois', texte: "trois", visible: true, typecarte:true, idcomplementaire: 11},
                {id: 4, Nom: 'quatre', texte: "quatre", visible: true, typecarte:true, idcomplementaire: 12},
                {id: 5, Nom: 'cinq', texte: "cinq", visible: true, typecarte:true, idcomplementaire: 13},
                {id: 6, Nom: 'six', texte: "six", visible: true, typecarte:true, idcomplementaire: 14},
                {id: 7, Nom: 'sept', texte: "sept", visible: true, typecarte:true, idcomplementaire: 15},
                {id: 8, Nom: 'huit', texte: "huit", visible: true, typecarte:true, idcomplementaire: 16},
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
<div >
    <div class="global" >
        <div class="entete">
         <h2 style="flex:1;">
            Jeu du mémo
        </h2>
            <div class="score">
                <h3>Nombre de coup : {{ coups }}</h3> 
            
                <h3>Temps : </h3>
            </div>
        </div>

        <div class=" page d-flex flex-column justify-center ">
          <div class="a">
            je suis une carte
          </div>
          <div class="b">
            je suis une carte
          </div>
          <div class="c">
            je suis une carte
          </div>
          <div class="d">
            je suis une carte
          </div>
          <div class="e">
            je suis une carte
          </div>
          <div class="f">
            je suis une carte
          </div>
          <div class="g">
            je suis une carte
          </div>
          <div class="h">
            je suis une carte
          </div>
          <div class="i">
            je suis une carte
          </div>
          <div class="j">
            je suis une carte
          </div>
          <div class="k">
            je suis une carte
          </div>
          <div class="l">
            je suis une carte
          </div>
          <div class="m">
            je suis une carte
          </div>
          <div class="n">
            je suis une carte
          </div>
          <div class="o">
            je suis une carte
          </div>
          <div class="p">
            je suis une carte
          </div>
        </div>

        <div class="entete">
            <div class="reponse">
                <h1> Reponse </h1>
            </div>

           <div>
           <img  src="src/icons8-flèche-haut-50.png">
           </div>

        </div>
    </div>
</div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
  
}
h3 {
  font-size: 1.2rem;
}

.page {
  display: grid;
  width: 100%;
  height: 100%;
  grid-template-areas:
    "a b c d"
    "e f g h"
    "i j k l"
    "m n o p";
  grid-template-rows: auto;
  grid-template-columns: auto;
}

.page > a {
  grid-area: a;
  background-color: #8ca0ff;
}

.page > b {
  grid-area: b;
  background-color: #ffa08c;
}

.page > c {
  grid-area: c;
  background-color: #ffff64;
}

.page > d {
  grid-area: d;
  background-color: #8cffa0;
}

.page > e {
  grid-area: e;
  background-color: #8cffa0;
}
.page > f {
  grid-area: f;
  background-color: #8cffa0;
}
.page > g {
  grid-area: g;
  background-color: #8cffa0;
}
.page > h {
  grid-area: h;
  background-color: #8cffa0;
}
.page > i {
  grid-area: i;
  background-color: #8cffa0;
}.page > j {
  grid-area: j;
  background-color: #8cffa0;
}
.page > k {
  grid-area: k;
  background-color: #8cffa0;
}
.page > l {
  grid-area: l;
  background-color: #8cffa0;
}
.page > m {
  grid-area: m;
  background-color: #8cffa0;
}
.page > n {
  grid-area: n;
  background-color: #8cffa0;
}
.page > o {
  grid-area: o;
  background-color: #8cffa0;
}
.page > p {
  grid-area: p;
  background-color: #8cffa0;
}
.score{
    display:flex;
     flex-direction: column; 
   align-items: flex-start; 
      justify-content:space-between; 
}
.global{
   display: flex; 
   flex-direction: column; 
   align-items: flex-start; 
   justify-content:space-between; 
   height: 100vh
}
.entete{
    display: flex; 
   flex-direction: row; 
   align-items: flex-start; 
    width:100%;
}

.reponse{
    flex: 1;
    text-align:center;
}
</style>
