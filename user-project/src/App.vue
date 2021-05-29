<template>
  <div id="app">  

    <button @click="loadUserData()">Get New User</button>
    <br/>

    <ag-grid-vue style="width: 800px; height: 700px;"
        class="ag-theme-alpine"
        :columnDefs="columnDefs"
        :rowData="rowData">
    </ag-grid-vue>
    
  </div>
</template>

<script>
    import { AgGridVue } from "ag-grid-vue";
    import axios from "axios";

    export default {
        name: 'App',
        data() {
            return {
                columnDefs: null,
                rowData: [],
                
          
            }
        },
        components: {
            AgGridVue
        },
        beforeMount() {
            this.columnDefs = [
    { field: 'id', sortable: true, filter: true },
    { field: 'name', sortable: true, filter: true },
    { field: 'url', sortable: true, filter: true }
];           
        },
        methods:{
          async loadUserData()
          {
     
          const response = await axios.get("https://localhost:44365/api/users/random");
          var responseData = 
          {
              id: response.data[0].id,
              name: response.data[0].name,
              url: response.data[0].url
          };
          this.rowData.push(responseData)

          }


        }
    }
</script>
<style lang="scss">
  @import "../node_modules/ag-grid-community/dist/styles/ag-grid.css";
  @import "../node_modules/ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>
