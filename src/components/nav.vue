<script>


export default {
  props: {
    page:"",
    changePageFetch: Function,
    pageSize: "",
  },

  data () {
    return {
      search: '',
    }
  },
  methods: {
    returnSearchData
  }
}

</script>

<template>
  <nav class="nav"> 
      <section class="Options">
        <select>
          <option class="default" value=""></option>
          <option value="">Filtro 2</option>
          <option value="">Filtro 1</option>
          <option value="">Filtro 1</option>
        </select>
      </section>
      <section class="input">
        <form>
          <i class="ri-search-line"></i>
          <input type="text" placeholder="Search" v-model="search" v-on:keyup.enter="searchData"/>
        </form>
      </section>
      <section class="pagination">
        <button class="button prev" v-on:click="changePageFetch( page - 1)">
          <img src="https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/icon.svg?alt=media&token=89c21e5e-9395-43ff-8833-59b4d350ff5e" alt="">
        </button>
        <p class="pages">{{ page }} / {{ pageSize }}</p>
        <button class="button next"  v-on:click="changePageFetch( page + 1)">
          <img src="https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/icon%20(1).svg?alt=media&token=c76c9e87-5ba1-41f8-ac3c-8870ea5fcb7f" alt="">
        </button>
      </section>
  </nav>
</template>

<style scoped>
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
  width: 40px;
  height: 32px;
}

.input form {
  display: grid;
  grid-template-columns: .2fr 2fr;
  width: 320px;
  height: 32px;
  background: #FFFFFF;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.06), 0px 0px 0px 1px rgba(104, 113, 130, 0.16);
  border-radius: 6px;
}

.input form input {
  border: none;
  outline: none;
  height: 90%;
  width: 90%;
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

.default {
  background: url("https://firebasestorage.googleapis.com/v0/b/emprendeyourlifestyle.appspot.com/o/filter.svg?alt=media&token=53735ece-37e1-49c1-8313-bb1782e98088");
}



@media screen and (max-width: 900px) {
  .nav {
    grid-template-columns: .3fr 1fr .3fr;
    
  }

  .input form {
    width: 90%;
  }

  .pagination {
     grid-template-areas: " prev page "
  " next page ";
    grid-gap: .6rem;
  }

  .pages {
    grid-area: page;
  }

  .prev {
    grid-area: prev;
  }

  .next {
    grid-area: next;
  }
} 


</style>

