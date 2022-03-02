<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import  Nav from './components/nav.vue';
import Info from './components/info.vue';

export default {
  components: {
    Nav,
    Info
  },
  data () {
    return {
      statePage: 0,
    }
  } 
}

</script>

<template>
  <div>
    <Nav :page="statePage"/>
    <Info @savePage="statePage = $event"/>
  </div>
</template>

<style>
:root {
  --color-background: rgba(244, 247, 252, 0.75);
  --color-nature: #fff;
  --font-family: 'Inter', sans-serif;
  --font-family-head: normal 600 11px/16px var(--font-family);
  --color-text: #464F60;
  
}


html, body {
  background: var(--color-nature);
  backdrop-filter: blur(8px);
  width: 100vw;
  height: auto;
  padding: 1rem 0;
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 80vw;
}

@media screen and (max-width: 900px) {
  #app {
    width: 90vw;
  }
}
  


</style>
