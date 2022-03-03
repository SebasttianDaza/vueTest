<script >
import axios from 'axios';
import Row from './row.vue';
/*

function 
}*/
export default {
  components: {
    Row
  },

  data () {
    return {
      infomation: [],
      informationGeneral: [],
      page: 1,
      pageSize: 1,

    }
  },

  methods: {
    async getData () {

      let AXIOS = axios;
      const params = {
        page: this.page
      }

      AXIOS.get("http://apitest.cargofive.com/api/ports", { params })
      .then(response => {
        
        this.pageSize = response.data.meta.last_page;
        this.page = response.data.meta.current_page;
        this.infomation = response.data.data;
        this.informationGeneral = response.data.data;
        this.$emit('savePage', this.page);
      })
      .catch(error => {
        console.log(error);
      });

      
    },

    changePage(page){
      this.page = (page <= 0 && page > this.pageSize) ? this.page : page;
      this.getData();
    }
  },

  mounted () {
    this.getData();
    this.$emit('changePage', this.changePage);
  }

}



</script>

<template>
  <table class="Table">
      <tr class="TableHead">
          <th>ID</th>
          <th>Name</th>
          <th>Country</th>
          <th>Continent</th>
          <th>Cordinates</th>
      </tr> 

      <Row v-for="(item, index) in infomation" :key="index" :nameIdentify="item.id" :nameContent="item.name" :country="item.country" :continent="item.continent" :cordinates="item.coordinates"></Row>     
  </table>
</template>

<style>
.Table {
  width: 100%;
  box-shadow: 0px 0px 0px 1px rgba(152, 161, 178, 0.1), 
  0px 1px 4px rgba(69, 75, 87, 0.12)
  , 0px 0px 2px rgba(0, 0, 0, 0.08);
  overflow:hidden;
  height: 100%;
}

.TableHead {
  font: var(--font-family-head);
  text-align: center;
  color: var(--colo-text);
  text-transform: uppercase;
  height: 40px;
  background-color: var(--color-background);
  backdrop-filter: blur(8px);
}


</style>