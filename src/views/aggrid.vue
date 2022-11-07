<template>
  
  <ag-grid-vue
    class="ag-theme-balham-dark"
    style="width: 1300px; height: 630px;" 
    :columnDefs="columnDefs.value"
    :rowData="rowData.value"
    :defaultColDef="defaultColDef"
    rowSelection="multiple"
    animateRows="true"
    pagination="true"
    paginationAutoPageSize=true

  >
  </ag-grid-vue>

  
</template>

<script>
import { AgGridVue } from "ag-grid-vue3";
import { reactive, onMounted } from "vue";
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-balham-dark.css";



export default {
  name: "App",
  components: { AgGridVue, },
  setup() {
    const rowData = reactive({
      value: [ {},],
    });

    const columnDefs = reactive({
      value: [{ field: "businessAccountNumber" }, { field: "businessName" }, { field: "businessType" }, 
      { field: "businessCity" },{ field: "salesEmployee" },{ field: "businessPhoneNumber" },
       { field: "businessLiquorLic" },{ field: "businessEmail" }],
    });

    const defaultColDef = {
      sortable: true,
      floatingFilter: true,
      filter:true
    };

    onMounted(() => {
      fetch("http://localhost:8888/business-accounts/all")
        .then((result) => result.json())
        .then((remoteRowData) => (rowData.value = remoteRowData)); 
    });

    return {
      columnDefs,
      rowData,
      defaultColDef,
    };

  },
};
</script>

<style lang="scss"></style>