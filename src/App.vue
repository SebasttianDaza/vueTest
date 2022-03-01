<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import  Nav from './components/nav.vue'
import table from './components/table.vue'
</script>

<template>
  <div>
    <Nav/>
  </div>
</template>

<style>
:root {
  --color-background: rgba(244, 247, 252, 0.75);
  --color-nature: #fff;
  
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
</style>
