<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

import Info from './components/info.vue';

export default {
  components: {
    Info
  },
  data () {
    return {
      nextPages: Function,
      prevPages: Function,
      search: '',
      searchDate: Function,
      typeSearch: 'name',
      pageTotal: 1,
      count: 1,
      placeholder: 'Search for name',
    }
  },
  methods: {
    dinamicPlaceholder () {
      if (this.typeSearch === 'name') {
        this.placeholder = 'Search for name'
      }
      if (this.typeSearch === 'country') {
        this.placeholder = 'Search for country'
      }
      if (this.typeSearch === 'continents') {
        this.placeholder = 'Search for continents'
      }
      
    },
  },
  mounted () {
    this.dinamicPlaceholder();
  }
}

</script>

<template>
  <div>
    <nav class="nav"> 
      <section class="Options">
        <select v-model="typeSearch">
          <option  class="default" value="name">Filter</option>
          <option value="name">Name</option>
          <option value="country">Country</option>
          <option value="continet">Continet</option>
        </select>
      </section>
      <section class="input">
        <div>
          <img src="https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/3844432_magnifier_search_zoom_icon.svg?alt=media&token=383ec967-4e06-44b3-a1fb-528c7dac3912" alt="">
          <input 
          v-model="search" 
          :placeholder="placeholder"
          v-on:keyup="searchDate(typeSearch)" 
          />
          
        </div>
      </section>
      <section class="pagination">
        <button class="button prev" v-on:click="prevPages()">
          <img src="https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/icon.svg?alt=media&token=89c21e5e-9395-43ff-8833-59b4d350ff5e" alt="">
        </button>
        <p class="pages"> {{ count }} / {{ pageTotal }}</p>
        <button class="button next"  v-on:click="nextPages()">
          <img src="https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/icon%20(1).svg?alt=media&token=c76c9e87-5ba1-41f8-ac3c-8870ea5fcb7f" alt="">
        </button>
      </section>
    </nav>

    <Info @nextPage="nextPages = $event" @prevPage="prevPages = $event" @searchData="searchDate = $event" :dataSearch="search"/>

    <section class="footer">
      <p>1</p>
      <p>1</p>
      <p>2</p>
      <p>3</p>
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

.nav {
  background-color: var(--color-background);
  backdrop-filter: blur(8px);
  box-shadow: 0px 0px 0px 1px rgba(152, 161, 178, 0.1), 
  0px 1px 4px rgba(69, 75, 87, 0.12)
  , 0px 0px 2px rgba(0, 0, 0, 0.08);
  height: 100px ;
  border-top-left-radius: .5rem;
  border-top-right-radius: .5rem;
  display: grid;
  grid-template-columns: .7fr 3fr 1fr;
  align-items: center;
}

.Options {
  justify-self: center;
}

.Options select {
  width: 60px;
  height: 32px;
}

.input div {
  display: grid;
  grid-template-columns: .2fr 2fr;
  width: 320px;
  height: 32px;
  background: #FFFFFF;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.06), 0px 0px 0px 1px rgba(104, 113, 130, 0.16);
  border-radius: 6px;
}

.input div input {
  border: none;
  outline: none;
  height: 90%;
  width: 90%;
}

.input div img {
  height: 22px;
  width: 22px;
  margin: auto;
}


.pagination {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  padding: .5rem;
  align-items: center;
  justify-items: center;
}

.button {
  width: 32px;
  height: 32px;
  background: #2264E6;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.06), 0px 0px 0px 1px rgba(104, 113, 130, 0.16);
  border-radius: 6px;
  border: none;
  outline: none;
  font: var(--font-family-body);
  cursor: pointer;
}

.button img {
  width: 50%;
  height: 50%;
  color: #FFFFFF;
  object-fit: contain;
}




@media screen and (max-width: 900px) {
  #app {
    width: 90vw;
  }

  .nav {
    grid-template-columns: .3fr .7fr .3fr;
    
  }

  .input div {
    width: 90%;
  }

  

  .pagination {
     grid-template-areas: " prev next ";
      grid-gap: .6rem;
  }

  .pages {
    display: none;
  }

  .prev {
    grid-area: prev;
  }

  .next {
    grid-area: next;
  }
} 

</style>
