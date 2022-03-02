<script >
   
   export default {
       props: {
            key: "",
            nameIdentify: "",
            nameContent: "",
            country: "",
            continent: "",
            cordinates: ""
       },
   }

    

</script>

<template>
      <tr class="tableRow" >
          <td> {{ nameIdentify }}</td>
          <td>{{ nameContent }}</td>
          <td>{{ country }}</td>
          <td>{{ continent }}</td>
          <td>{{ cordinates }}</td>
      </tr>     
</template>

<style>
.tableRow {
  width: 100%;
  text-align: center;
  height: 40px;
}

</style>

