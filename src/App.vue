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
      statePage: 1,
      changePageComplete: Function,
      savePageTotal: 25,
      searchDatas: Function,
    }
  } 
}

</script>

<template>
  <div>
    <Nav :page="statePage" :changePageFetch="changePageComplete" :pageSize="savePageTotal" :searchData="searchDatas"/>
    
    <Info @savePage="statePage = $event" @changePage="changePageComplete = $event" @savePageSize="savePageTotal = $event" @searchData="searchDatas = $event"/>

    <section class="footer">
      <p>{{ statePage }}</p>
      <p>{{ statePage }}</p>
      <p>{{ statePage }}</p>
      <p>{{ statePage }}</p>
    </section>
  </div>
</template>

<style>

:root {
  --color-background: rgba(244, 247, 252, 0.75);
  --color-nature: #fff;
  --font-family: 'Inter', sans-serif;
  --font-family-head: normal 600 11px/16px var(--font-family);
  --font-family-body: normal 500 14px/20px var(--font-family);
  --color-text: #464F60;
  --color-text-second: #171C26;
  
}


html, body {
  background: var(--color-nature);
  backdrop-filter: blur(8px);
  width: 100%;
  height: auto;
  padding: 1rem 0;
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 80%;
}

.footer {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  width: 100%;
  height: 35px;
  padding: 1rem 0;
  margin: 0;
  background-color: var(--color-background);
  backdrop-filter: blur(8px);
  box-shadow: 0px 0px 0px 1px rgba(152, 161, 178, 0.1), 
  0px 1px 4px rgba(69, 75, 87, 0.12)
  , 0px 0px 2px rgba(0, 0, 0, 0.08);
  border-bottom-left-radius: .5rem;
  border-bottom-right-radius: .5rem;
  align-items: center;
  justify-content: center;
  text-align: center;
}

@media screen and (max-width: 900px) {
  #app {
    width: 90vw;
  }
}
  


</style>
