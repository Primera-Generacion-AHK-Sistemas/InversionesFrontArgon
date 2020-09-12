<template>
  <b-card no-body>
    <b-card-header class="border-0">
      <h3 class="mb-0">CEDEARS</h3>
    </b-card-header>

    <b-table
      id="my-table"
      :items="items"
      :fields="fields"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      sort-icon-left
      responsive="lg"
      :per-page="perPage"
      :current-page="currentPage"
    >
      <template v-slot:cell(acciones)="row">
        <b-button
          pill
          variant="success"
          size="sm"
          v-on:click="detalle(row.id)"
          class="mr-2"
        >Detalles</b-button>
        <b-button
          pill
          variant="success"
          size="sm"
          v-on:click="agregar"
          class="mr-2"
        >Agregar</b-button>
      </template>
    </b-table>

    <b-card-footer class="py-4">
      <div>
        <b-pagination
          v-model="currentPage"
          pills
          size="md"
          hide-goto-end-buttons
          :total-rows="rows"
          :per-page="perPage"
          align="center"
          aria-controls="my-table"
        ></b-pagination>
      </div>
    </b-card-footer>
  </b-card>
</template>

<script>
import json from "../../../../public/response.json";

export default {
  data() {
    return {
      perPage: 10,
      currentPage: 1,
      sortBy: "id",
      sortDesc: false,
      fields: [
        //{ key: "id", sortable: true },
        //{ key: "assetType", sortable: false },
        { key: "ticker", label: "Nombre", sortable: true },
        { key: "description", label: "Descripcion", sortable: true },
        { key: "acciones", label: "", sortable: false },
      ],
      items: json,
    };
  },
  methods: {
    detalle(id) {
      console.log(id);
    },
    agregar() {
      console.log('Agregar');
    },
  },
  computed: {
    rows() {
      return this.items.length;
    },
  },
};
</script>
