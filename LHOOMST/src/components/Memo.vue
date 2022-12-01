<script >
export default {
    data() {
        return {
      coups: 0,
      temps: 0,
        }
    },
    methods: {

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

        <div class=" justify-center ">
        je suis le centre
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
