<template>

  <main>
    <div>
      <img alt="Vue logo" v-on:click="refresh()"  class="logo" src="./assets/timeMachine.jpg" width="76" height="41" />
    </div>
    <div>
      Sequence: {{info.seq}}
    </div>
    <div>
      Scores: {{info.score}}
    </div>
    <div>
      <button v-on:click="action('modeAnnee')" :style="info.mode==0?'font-weight: bold':''">Capitaines</button>
      <button v-on:click="action('modeQuiz')" :style="info.mode==1?'font-weight: bold':''">Quiz</button>
      <button v-on:click="action('modeQuiz2026' )":style="info.mode==2?'font-weight: bold':''" >Quiz 2026</button>

    </div>
    <div>
      <button v-on:click="action('prev')">Précédent</button>
      <button v-on:click="action('next')">Suivant</button>
      <button v-on:click="action('nextQuestion')">Question suiv</button>

    </div>
    <div align="center">Equipes</div>
    <div class="grid-container">
    <div v-for="(equipe,index) in equipes" >
      <button v-on:click="action('setEquipe/' + index)" :style="info.equipe==index?'font-weight: bold':''">  {{ equipe }}</button>
    </div>
    </div>
        <div align="center">Actions</div>
    <div><button v-on:click="action('ventilo/1/on')">Ventilo On</button><button v-on:click="action('ventilo/1/off')">Ventilo Off</button></div>
    <div><button v-on:click="action('voltmetre/on')">Voltmetre On</button><button v-on:click="action('voltmetre/off')">Voltmetre Off</button></div>
    <div><button v-on:click="action('convecteur/on')">Convecteur On</button><button v-on:click="action('convecteur/off')">Convecteur Off</button></div>
    <div><button v-on:click="action('neon/1/on')">Hello On</button><button v-on:click="action('neon/1/off')">Hello Off</button></div>
    <div><button v-on:click="action('neon/2/on')">Smile On</button><button v-on:click="action('neon/2/off')">Smile Off</button></div>
    <div><button v-on:click="action('neon/3/on')">Dream On</button><button v-on:click="action('neon/3/off')">Dream Off</button></div>
    <div><button v-on:click="action('neon/4/on')">Arc en ciel On</button><button v-on:click="action('neon/4/off')">Arc en ciel Off</button></div>
    <div>
     {{msg}}
     </div>
  </main>
</template>

<script language="javascript">
import axios from 'axios'
export default {
  data() {
    return {
      info: {},
      equipes: ["1998","1965","1976","2011","1981","2000"],
      msg:""
    };
  },
  methods: {
    refresh() {
    axios
      .get(import.meta.env.VITE_API_URL+"info")
      .then(response => {
          console.log(response);
          this.info = response.data;
          })
      .catch(error => {
           // handle error
           console.log(error);
           this.setMessage(error);
      })
   },
   action(type) {
    console.log(import.meta.env.VITE_API_URL + type);
    axios
      .get(import.meta.env.VITE_API_URL + type)
      .then(response => {
        console.log(response.data);
        this.setMessage(response.data);
        //this.refresh();
          })
      .catch(error => {
       // handle error
       console.log(error);
       this.setMessage(type + " : " +  error);
     })
    },
    setMessage(msg) {
      this.msg = msg
      setTimeout(() => this.msg="", 2000)
    }
  },
  mounted () {
  console.log(navigator.userAgent)
    this.refresh()
  },
  created () {

  }
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

:global(corps) {
  bgcolor : white ;
}

button {
  width: 120px;
  height: 40px;
}

buttonGras {
  width: 120px;
  height: 40px;
  font-weight: bold;
  color : red;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* Crée 2 colonnes égales */
  /*gap: 10px;  Espace entre les colonnes et lignes */
}

.grid-item {
  border: 1px solid #ccc;
  padding: 20px;
}
</style>
