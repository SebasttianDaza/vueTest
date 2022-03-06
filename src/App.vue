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
      typeSearch: '',
      resultsTotal: {
        type: Number,
        default: 0
      },
    }
  }

}

</script>

<template>
  <div>
    <nav class="nav"> 
      <section class="Options" required>
        <select v-model="typeSearch" id="select">
          <option disabled hidden selected>Select</option>
          <option value="name">Name</option>
          <option value="country">Country</option>
          <option value="continet">Continet</option>
        </select>
      </section>
      <section class="input">
        <div>
          <i class="bi bi-search"></i>
          <input 
          v-model="search" 
          :placeholder="( typeSearch === 'name' ) ? 'Search by name' : ( typeSearch === 'country' ) ? 'Search by country' : 'Search by continent' "
          v-on:keyup="searchDate(typeSearch)" 
          />
        </div>
      </section>
      <section class="pagination">
        <button class="button prev" v-on:click="prevPages()">
          <i class="bi bi-arrow-left"></i>
        </button>
        <button class="button next"  v-on:click="nextPages()">
          <i class="bi bi-arrow-right"></i>
        </button>
      </section>
    </nav>

    <Info @nextPage="nextPages = $event" @prevPage="prevPages = $event" @searchData="searchDate = $event" :dataSearch="search"  @countELement="resultsTotal = $event"/>

    <section class="footer">
      <p>Results: {{  resultsTotal  }}</p>
      <p>Sebastian Daza</p>
      <p>Carbon Five</p>
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
  --font-family-footer: normal 500 12px/18px var(--font-family);
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
  grid-template-columns: repeat(3, 1fr);
  width: 100%;
  min-height: 35px;
  max-height: 35px;
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
  font: var(--font-family-footer);
  color: var(--color-text-second);
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

#select {
  appearance: none;
  color: var(--color-text-second);
  outline: 0;
  font: var(--font-family-body);
  /* Personalize */
  width: 60px;
  height: 32px;
  padding: 0 4em 0 1em;
  border-radius: 0.25em;
  box-shadow: 0 0 1em 0 rgba(0, 0, 0, 0.2);
  cursor: pointer;
  
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

.input div:hover {
  box-shadow: 0 0 1em 0 rgba(0, 0, 0, 0.2);
}

.input div input {
  border: none;
  outline: none;
  height: 90%;
  width: 90%;
}

.input div i {
  height: 22px;
  width: 22px;
  margin: auto;
}


.pagination {
  display: grid;
  grid-template-columns: 1fr 1fr ;
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

.button i {
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
    grid-gap: 1rem;
  }

} 

</style>
