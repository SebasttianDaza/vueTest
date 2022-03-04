<script >
import axios from 'axios';
import Row from './row.vue';

export default {
  components: {
    Row
  },

  props: {
    dataSearch: "",
  },

  data () {
    return {
      infomation: [],
      informationGeneral: [],
      page: 0,
      pageSize: 0,
      filterInfo: [],
    }
  },

  methods: {
    async getData () {
  
      let AXIOS = axios;
      const URL = "http://apitest.cargofive.com/api/ports?page=" ;
      const page = [];

      for (let i = 1; i < 25; i++) {
        page.push(URL + i);
      }


      await AXIOS.all( page.map(url => AXIOS.get(url)) )
        .then(AXIOS.spread((...responses) => {
          responses.forEach(response => {
            this.infomation = this.infomation.concat(response.data.data);
            this.informationGeneral = this.informationGeneral.concat(response.data.data);
          });
        }))

      
        
    },
      
    nextPage(){
      console.log("nextPage");
      this.page = this.page + 10;
    },
    prevPage(){
      if (this.page > 0) {
        this.page = this.page - 10;
      }
    },
      
    searchData (type) {
      this.page = 1;
      if(type === "name"){
        this.infomation = this.informationGeneral.filter(item => {
          if(item.name.toLowerCase().includes(this.dataSearch.toLowerCase())){
            return item;
          }
        });
      }
      if(type === "country"){
        this.infomation = this.informationGeneral.filter(item => {
          if(item.country.toLowerCase().includes(this.dataSearch.toLowerCase())){
            return item;
          }
        });
      }
      if(type === "continet"){
        this.infomation = this.informationGeneral.filter(item => {
          if(item.continent.toUpperCase().includes(this.dataSearch.toUpperCase())){
            return item;
          }
        });
      }
      
    }
  },

  mounted () {
    this.getData();
    this.$emit('nextPage', this.nextPage);
    this.$emit('prevPage', this.prevPage);
    this.$emit('searchData', this.searchData);
  }

}


</script>

<template>
  <div class="contentTable">
    <table class="Table">
      <tr class="TableHead">
          <th class="thId">ID</th>
          <th class="thName">Name</th>
          <th class="thCountry">Country</th>
          <th class="thContinent">Continent</th>
          <th class="thCoordinates">Coordinates</th>
      </tr> 
      

      <Row 
      v-for="(item, index) in infomation.slice(page, page + 10)" 
      :key="index" 
      :nameIdentify="item.id" 
      :nameContent="item.name" 
      :country="item.country" 
      :continent="item.continent" 
      :cordinates="item.coordinates"
      
       >
      </Row>     

  </table>
  </div>
</template>

<style>
.contentTable {
  overflow: auto;
  width: 100%;
  overflow-y: auto;
  box-shadow: 0px 0px 0px 1px rgba(152, 161, 178, 0.1), 
  0px 1px 4px rgba(69, 75, 87, 0.12)
  , 0px 0px 2px rgba(0, 0, 0, 0.08);
}

.Table {
  width: 100%;
  border-collapse: collapse;
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
  width: 100%;
}

.thId {
  width: 10%;
}

.thName {
  width: 30%;
}

.thCountry {
  width: 20%;
}

.thCoordinates {
  width: 30%;
}

.thContinent {
  width: 10%;
}

</style>