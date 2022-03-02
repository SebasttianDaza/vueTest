<script setup>
  

</script>

<template>
  <nav class="nav"> 
      <section class="Options">
        <select>
          <option value=""></option>
          <option value="">Filtro 2</option>
          <option value="">Filtro 1</option>
          <option value="">Filtro 1</option>
        </select>
      </section>
      <section class="input">
        <form>
          <i class="ri-search-line"></i>
          <input type="text" placeholder="Search" />
        </form>
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
  height: 90px ;
  border-top-left-radius: .5rem;
  border-top-right-radius: .5rem;
  display: grid;
  grid-template-columns: .7fr 4fr;
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


@media screen and (max-width: 900px) {
  .nav {
    grid-template-columns: .7fr 3fr;
    
  }

  .input form {
    width: 90%;
  }
} 


</style>

