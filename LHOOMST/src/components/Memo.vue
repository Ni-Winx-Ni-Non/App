<script>
export default {
    data() {
        return {
          coups: 0,
      temps: 0, 
      idcarte1:-1,
      idcarte1Select: -1,
      idcarte2Select: -1,
            cartes: [
                {id: 1, Nom: 'Chlamydia', texte: "CHText", visible: 0, typecarte:true},
                {id: 2, Nom: 'Condylome', texte: "ConText", visible: 0, typecarte:true},
                {id: 3, Nom: 'trois', texte: "troisTex", visible: 0, typecarte:true},
                {id: 4, Nom: 'quatre', texte: "quatreTex", visible: 0, typecarte:true},
                {id: 5, Nom: 'cinq', texte: "cinqTex", visible: 0, typecarte:true},
                {id: 6, Nom: 'six', texte: "sixTex", visible: 0, typecarte:true},
                {id: 7, Nom: 'sept', texte: "septTex", visible: 0, typecarte:true},
                {id: 8, Nom: 'huit', texte: "huitTex", visible: 0, typecarte:true},
            ],
            carteFinal: [],
        }
    },
    methods: {
        clickCarte(id) {
            this.coups++;
            if(this.idcarte1==-1){ //ça veut dire qu'il n'y a pas de carte retournée
                //On retourne la carte
                this.idcarte1Select = id
                this.idcarte1= this.carteFinal[id].id; // on récupère l'id complémentaire
                this.carteFinal[id].visible=1
            }
            else if (this.idcarte1Select != id){ //ça veut dire qu'il y a déjà une carte de retournée
                //On retourne la carte
                this.idcarte2Select = id;
                this.carteFinal[id].visible=1
                if(this.carteFinal[id].id==this.idcarte1) {//les cartes match
                    this.carteFinal[this.idcarte1Select].visible=2
                    this.carteFinal[id].visible=2
                    this.idcarte1=-1
                    this.idcarte1Select = -1
                    this.idcarte2Select = -1 
                    console.log("Win")
                }
                else{ //Les cartes match pas
                    
                    setTimeout(() => {
                        this.carteFinal[this.idcarte1Select].visible=0
                    this.carteFinal[id].visible=0
                    this.idcarte1=-1
                    this.idcarte1Select = -1
                    this.idcarte2Select = -1   
                    }, 500000);
                    console.log("Lose")
                }
            }
            
        }
    },
    mounted() {
        console.log('Shuffle card')
        for (let i = 0; i < 2; i++) {
            for (let j = 0; j < this.cartes.length; j++) {
                if (i == 0) {
                    let copy = JSON.stringify(this.cartes[j])
                    this.carteFinal.push(JSON.parse(copy))
                    this.carteFinal[j].typecarte = false
                } else {
                    this.carteFinal.push(this.cartes[j])
                }
            }
        }
        console.log(JSON.stringify(this.carteFinal))
        this.carteFinal = this.carteFinal.sort((a, b) => 0.5 - Math.random());
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
                <h3>Nombre de coups : {{ coups }}</h3> 
            
                <h3>Temps : </h3>
            </div>
        </div>

        <div class=" page d-flex flex-column justify-center ">
          <div v-for="(item, index) in carteFinal" :key="index" class="a">
            <div v-if="item.visible==1">
                <p @click="clickCarte(index)" :style="idcarte1Select == index  || idcarte2Select == index ? 'border: 1px solid #252525' : ''" v-if="item.typecarte">{{ item.Nom }}</p>
                <p @click="clickCarte(index)" :style="idcarte1Select == index || idcarte2Select == index ? 'border: 1px solid #252525' : ''" v-else>{{ item.texte }}</p>
            </div>
            <div v-else-if="item.visible==0" style="align-self: center;">
                 <img  @click="clickCarte(index)" style=" max-width: 100%; border: 2px solid #FFC6C0" src="src/314380334_1154748302131982_231124094073081350_n.jpg">
            </div>
          </div>
          
        </div>
        <div class="texterep" >
          <div v-if=" idcarte1Select != -1 && !this.carteFinal[idcarte1Select].typecarte && this.carteFinal[idcarte1Select].visible == 1 ">
          {{  carteFinal[idcarte1Select].texte}}
          </div>
          <div v-if=" idcarte2Select != -1 && !this.carteFinal[idcarte2Select].typecarte && this.carteFinal[idcarte2Select].visible == 1 ">
          {{ carteFinal[idcarte2Select].texte }}
          </div>
          </div>
        <div class="entete">
            <div class="reponse">
                <h1> Réponse </h1>
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
.texterep{
    display: flex;
    align-items: flex-start;
    justify-content:space-between;
    width:100%;
}
.page {
  display: grid;
  width: 100%;
  height: 100%;
  grid-template-columns: repeat(4, minmax(0, 1fr))
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
   height: 100vh;
   background-color:#FFC6C0; 
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
.a{
    display:flex;
    align-items:center;
}

</style>
