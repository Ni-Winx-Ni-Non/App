<script>
export default {
    data() {
        return {
          coups: 0,
      temps: 0,
      reponse:false,
      idcarte1:-1,
      idcarte1Select: -1,
      idcarte2Select: -1,
      nom:[],
      victoire:0,
            cartes: [
                {id: 1, Nom: 'Chlamydiose', texte: "Souvent asymptomatque. Symptômes femmes: brûlure en urinant, écoulements anormaux de l'anus, douleurs abdominales, spotting, saignements ou écoulements anormaux entre les règles, douleur aux rapports sexuels. Symptômes homme: brûlure en urinant, gonflement/douleur des testicules, démangeaisons de l'urètre, inflamation du rectum", visible: 0, typecarte:true},
                {id: 2, Nom: 'VIH', texte: "Longue phase sans signe apparent, mais pendant laquelle le virus est présent dans l’organisme et, en l’absence de traitement, peut être transmis. Le seul moyen de diagnostic est un despistage régulier. Sans traitement approprié, ce virus affaiblit progressivement le système immunitaire.", visible: 0, typecarte:true},
                {id: 3, Nom: 'Gardnerella vaginalis', texte: "Atteint rarement et de manière asymptomatique les hommes. Pour les femmes les symptômes sont des pertes blanches grisâtre et fluide. Elle peut conduire à une vaginose et se transformer en vaginite ou vulvite", visible: 0, typecarte:true},
                {id: 4, Nom: 'Gonococcie', texte: "Aussi appelé chaude-pisse. Se transmet lors de rapport non protégés. Symptômes chez l'homme : écoulement de pus par la verge, brûlures urinaires. Souvent asymptomatique chez la femme, on peut tout de même observer des démengeaisons, des douleurs au rapport, des brûlures en urinant.", visible: 0, typecarte:true},
                {id: 5, Nom: 'Herpès génital', texte: "Virus qui reste à vie dans l'organisme et se manifeste par des poussées. Les symptômes sont des petites vésicules qui peuvent brûler ou démanger", visible: 0, typecarte:true},
                {id: 6, Nom: 'Morpions', texte: "Petits insectes noirs qui transmettent la phtiriase. Symptômes: démangeaisons", visible: 0, typecarte:true},
                {id: 7, Nom: 'Trichomonase', texte: "Causée par un parasite. Se transmet aussi en partageant le linge de toilette ou les sous-vêtements. Peut causer une vaginite ou une urétrite.", visible: 0, typecarte:true},
                {id: 8, Nom: 'Syphilis', texte: "Causée par une bactérie. Évolue en trois stade : 1) Lésion ronde, unique, dure et non douloureuse sur les parties générale. 2) Lésions rose pale ou brunes qui semble peler pouvant toucher le corps entier. 3) Complications tardives dues à une non détection", visible: 0, typecarte:true},
            ],
            carteFinal: [],
        }
    },
    methods: {
    reset () { 
      this.coups= 0
      this.temps= 0
      this.reponse=false
      this.idcarte1=-1
      this.idcarte1Select= -1
      this.idcarte2Select= -1
      this.nom=[]
      this.victoire=0
      this.carteFinal= []
    },
    clickreponse () { 
        this.reponse=!this.reponse;
    },
        clickCarte(id) {
            if (this.idcarte2Select == -1) {
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
                        this.nom.push(id)
                        this.idcarte1=-1
                        this.idcarte1Select = -1
                        this.idcarte2Select = -1 
                        console.log("Win")
                        for (let j = 0; j < this.carteFinal.length; j++){
                            if(this.carteFinal[j].visible==2){
                            this.victoire = this.victoire+2;}
                        }
                        if(this.victoire==32){
                            
                        }
                        else {
                            this.victoire=0;
                        }
                    }
                    else{ //Les cartes match pas
                        
                        setTimeout(() => {
                            this.carteFinal[this.idcarte1Select].visible=0
                        this.carteFinal[id].visible=0
                        this.idcarte1=-1
                        this.idcarte1Select = -1
                        this.idcarte2Select = -1   
                        }, 1000);
                        console.log("Lose")
                    }
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
            
            </div>
            <div v-if="victoire==32">
                <button @click="($emit('endMemo',{result:coups}),reset())">Continuez</button>
            </div>
        </div>
         <div>Associez les infections avec leurs descriptions. Pour cela, cliquez d'abord sur une carte rose, lisez la description puis tentez de trouver la carte bleue correspondante.</div>
        <div v-if="reponse" class="listereponse">
            <div v-for="item in nom" >
                  <p  v-if="carteFinal[item].visible==2" style="text-decoration: underline;">{{ carteFinal[item].Nom }} :</p>
                   <p  v-if="carteFinal[item].visible==2">{{carteFinal[item].texte}}</p>
            </div>
        </div>
        <div v-else class=" page d-flex flex-column justify-center ">
          <div v-for="(item, index) in carteFinal" :key="index" class="a">
            <div v-if="item.visible==1">
                <p  v-if="item.typecarte">{{ item.Nom }}</p>
                <p  v-else> Texte carte     </p>
            </div>
            <div v-else-if="(item.visible==0 && !item.typecarte)" style="align-self: center; border-radius:2rem;" class="a">
                 <img  @click="clickCarte(index)" style=" max-width: 60%; background-color:#fc9e8b " src="../assets/logoapp.png">
            </div>
            <div v-else-if="(item.visible==0 &&item.typecarte)" style="align-self: center; border-radius:2rem;" class="a">
                 <img  @click="clickCarte(index)" style=" max-width: 60%; background-color:#cafcf7 " src="../assets/logoapp.png">
            </div>
          </div>
          
        </div>
        <div class="texterep" >
          <div v-if=" idcarte1Select != -1 && !this.carteFinal[idcarte1Select].typecarte && this.carteFinal[idcarte1Select].visible == 1 ">
          Carte 1: 
          {{  carteFinal[idcarte1Select].texte}}
          </div>
          <div v-if=" idcarte2Select != -1 && !this.carteFinal[idcarte2Select].typecarte && this.carteFinal[idcarte2Select].visible == 1 ">
          Carte 2 : 
          {{ carteFinal[idcarte2Select].texte }}
          </div>
          </div>
        <div class="rep">
            <div class="reponse">
                <h2> Réponse </h2>
            </div>

           <div v-if="reponse" @click="clickreponse() ">
           <img  src="../assets/bas.png">
           </div>
           <div v-else @click="clickreponse() ">
           <img  src="../assets/haut.png">
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
.listereponse{
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
   background-color:#8DB0B9; 
   padding: 2rem; 
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
    justify-content: center;
}
.rep{
     display: flex; 
   flex-direction: row; 
   align-items: flex-start; 
    width:100%;
    border:1px solid;
    border-color:#000000;
    border-radius:10px;
}
</style>