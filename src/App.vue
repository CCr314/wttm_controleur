<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/timeMachine.jpg" width="76" height="41" />
  </header>

  <main>
    <div>
       {{info}}
       {{info.score}}


    </div>
    <div>
      <button v-on:click="action('prev')">Précédent</button>
      <button v-on:click="action('next')">Suivant</button>
    </div>
    <div v-for="equipe in equipes" >
      <button v-on:click="action('setEquipe/' + equipe.key)">  {{ equipe }}</button>
    </div>
    <div><button v-on:click="action('ventillo/1/on')">Ventillo On</button><button v-on:click="action('ventillo/1/off')">Ventillo Off</button></div>
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
      info: "",
      equipes: ["1998","1965","1976","2011","1981","2000"],
      msg:""
    };
  },
  methods: {
    refresh() {
    axios
      .get(import.meta.env.VITE_API_URL+"info")
      .then(response => {
        console.log(response.data);
          this.info = response.data.json;
          console.log(this.info.seq)
          })
      .catch(error => {
           // handle error
           console.log(error);
           this.setMessage(error);
      })
   },
   action(type) {
    axios
      .get(import.meta.env.VITE_API_URL + type)
      .then(response => {
        console.log(response.data);
        this.setMessage(response.data);
        this.refresh();
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

</style>
