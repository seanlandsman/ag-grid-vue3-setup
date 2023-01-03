<template>
  <ag-grid-vue
      class="ag-theme-alpine"
      style="height: 500px"
      :columnDefs="columnDefs.value"
      :rowData="rowData.value"
      :defaultColDef="defaultColDef"
      :frameworkComponents="frameworkComponents"
      rowSelection="multiple"
      animateRows="true"
  >
  </ag-grid-vue>
</template>

<script setup>
import {AgGridVue} from "ag-grid-vue3";
import MyComponent from "./components/MyComponent.vue"
import {reactive, onMounted, ref} from "vue";

import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-alpine.css";

const rowData = reactive({});

const columnDefs = reactive({
  value: [
    {field: "make"},
    {field: "model"},
    {field: "price", cellRendererFramework: 'MyComponent'}
  ],
});

const defaultColDef = {
  flex: 1
};

const frameworkComponents = {
  MyComponent
}

// Example load data from sever
onMounted(() => {
  fetch("https://www.ag-grid.com/example-assets/row-data.json")
      .then((result) => result.json())
      .then((remoteRowData) => (rowData.value = remoteRowData));
});

</script>

<style lang="scss"></style>


<!--

<template>
  <button @click="deselectRows">deselect rows</button>
  <ag-grid-vue
      class="ag-theme-alpine"
      style="height: 500px"
      :columnDefs="columnDefs.value"
      :rowData="rowData.value"
      :defaultColDef="defaultColDef"
      rowSelection="multiple"
      animateRows="true"
      :frameworkComponents="frameworkComponents"
      @cell-clicked="cellWasClicked"
      @grid-ready="onGridReady"
  >
  </ag-grid-vue>
</template>

<script>
import {AgGridVue} from "ag-grid-vue3";  // the AG Grid Vue Component
import {reactive, onMounted, ref} from "vue";

import "ag-grid-community/styles/ag-grid.css"; // Core grid CSS, always needed
import "ag-grid-community/styles/ag-theme-alpine.css"; // Optional theme CSS

const MyComponent = {
  template: '<span>My Component: {{ this.params.value }}</span>',
}


export default {
  name: "App",
  components: {
    AgGridVue,
    // MyComponent
  },
  setup() {
    const gridApi = ref(null); // Optional - for accessing Grid's API

    // Obtain API from grid's onGridReady event
    const onGridReady = (params) => {
      gridApi.value = params.api;
    };

    const frameworkComponents = {
      MyComponent
    }

    const rowData = reactive({}); // Set rowData to Array of Objects, one Object per Row

    // Each Column Definition results in one Column.
    const columnDefs = reactive({
      value: [
        {field: "make"},
        {field: "model"},
        {field: "price", cellRendererFramework: 'MyComponent'}
      ],
    });

    // DefaultColDef sets props common to all Columns
    const defaultColDef = {
      sortable: true,
      filter: true,
      flex: 1
    };

    // Example load data from sever
    onMounted(() => {
      fetch("https://www.ag-grid.com/example-assets/row-data.json")
          .then((result) => result.json())
          .then((remoteRowData) => (rowData.value = remoteRowData));
    });

    return {
      onGridReady,
      columnDefs,
      rowData,
      defaultColDef,
      frameworkComponents,
      cellWasClicked: (event) => { // Example of consuming Grid Event
        console.log("cell was clicked", event);
      },
      deselectRows: () => {
        gridApi.value.deselectAll()
      }
    };
  },
};
</script>

<style lang="scss"></style>
-->
