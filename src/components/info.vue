<script >
import axios from 'axios';
import Row from './row.vue';
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';

export default {
  components: {
    Row,
    Loading
  },

  props: {
    dataSearch: "",
  },

  data () {
    return {
      infomation: [],
      informationGeneral: [],
      page: 0,
      countELement: 0,
      isLoading: false,
      findNotError: true,
    }
  },

  methods: {
    //Get data of the API
    async getData () {
  
      let AXIOS = axios;
      const URL = "http://apitest.cargofive.com/api/ports?page=" ;
      const page = [];

      for (let i = 1; i < 25; i++) {
        page.push(URL + i);
      }

      this.isLoading = true;

      await AXIOS.all( page.map(url => AXIOS.get(url)) )
        .then(AXIOS.spread((...responses) => {
          responses.forEach(response => {
            this.infomation = this.infomation.concat(response.data.data);
            this.informationGeneral = this.informationGeneral.concat(response.data.data);
            this.countELement = response.data.meta.total;
            this.$emit('countELement', this.countELement);
          });
        }))
        .catch(error => {
          this.handleError(error);
        });

      this.isLoading = false;
      

      
        
    },
    
    //Get next page
    nextPage(){
      if (this.informationGeneral.filter(item => item.name.toLowerCase().includes(this.dataSearch.toLowerCase())).length > this.page + 10) {
        this.page = this.page + 10;
      } 
      
    },

    //Get prev page
    prevPage(){
      if (this.page > 1) {
        this.page = this.page - 10;
      }
    },
      
    //Get the data to search  
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
      
    },

    handleError (error) {
      console.warn(error)
      if(error.response.status === 429){
        this.findNotError = false;
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

<template >
  

  <div class="contentTable">
    <table class="Table">
      <tr class="TableHead">
          <th class="thId">ID</th>
          <th class="thName">Name</th>
          <th class="thCountry">Country</th>
          <th class="thContinent">Continent</th>
          <th class="thCoordinates">Coordinates </th>
      </tr> 
      <loading 
        :active='isLoading' 
        :is-full-page="false" 
        loader="bars"
        z-index="9999"
        lock-scroll="true"

      />

      {{
        findNotError === true ? '' : 'No results found, reload the page'
      }}
      
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
  min-height: 400px;
}

div.showError {
  display: block;
}

div.handleError {
  display: none;
  opacity: 0;
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