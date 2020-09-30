<template>
  <div id="app">
    <component-pokemon></component-pokemon>
  </div>
</template>

<script>
import Pokemon from "./components/Pokeguia.vue";
  export default {
    data() {
      return {
        message: 'Hola en vue',
      };
    },
    components:{
      'component-pokemon': Pokemon,
    }

  }
</script>

<style scoped>
  #app {
   
  }
</style>
