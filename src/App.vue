<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/timeMachine.jpg" width="76" height="41" />
  </header>
  <br>
     {{info}}
 <br>
  <main>
    <button v-on:click="action('prev')">Précédent</button>
    <button v-on:click="action('next')">Suivant</button>
  <br>
     {{msg}}
  </main>
</template>

<script language="javascript">
import axios from 'axios'
export default {
  data() {
    return {
      info: "",
      msg:""
    };
  },
  methods: {
    refresh() {
    axios
      .get(import.meta.env.VITE_API_URL+"info")
      .then(response => {
        console.log(response.data);
          this.info = response.data;
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

</style>
