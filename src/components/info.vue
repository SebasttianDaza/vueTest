<script >
import Row from './row.vue';

async function methods () {
   
      fetch('https://api.covid19api.com/summary')
        .then(response => response.json())
        .then(data => {
          console.log(data);
        });
}

methods();


export default {
  components: {
    Row
  },
  props: {
    data: {
      type: Array,
      required: true
    }
  },
  methods: {
    async fetchData() {
      fetch('https://api.covid19api.com/summary')
        .then(response => response.json())
        .then(data => {
          this.data = data.Countries;
        });
    },
  },
  created() {
    this.fetchData();
  }
};


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
      <Row :data="data"/>    
  </table>
</template>

<style>
.Table {
  width: 100%;
  box-shadow: 0px 0px 0px 1px rgba(152, 161, 178, 0.1), 
  0px 1px 4px rgba(69, 75, 87, 0.12)
  , 0px 0px 2px rgba(0, 0, 0, 0.08);
  overflow:hidden;
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