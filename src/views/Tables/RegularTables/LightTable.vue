<template>
  <b-card no-body>
    <b-card-header class="border-0">
      <b-container>
        <b-row>
          <b-col sm="6"><h2>CEDEARS</h2></b-col>
          <b-col sm="6">
            <b-input-group class="mt-2">
              <b-form-input v-model="keyword" placeholder="Buscar" type="text"></b-form-input>
              <b-input-group-append>
                <b-button :disabled="!keyword" size="sm" @click="keyword = ''" variant="info">
                  <b-icon icon="x-circle-fill"></b-icon>
                </b-button>
              </b-input-group-append>
            </b-input-group>
          </b-col>
        </b-row>
      </b-container>
    </b-card-header>

    <b-table
      id="my-table"
      :cedears="cedears"
      :fields="fields"
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      sort-icon-left
      responsive="lg"
      :per-page="perPage"
      :current-page="currentPage"
      :keyword="keyword"
      :items="items"
    >
      <template v-slot:cell(acciones)="row">
        <b-button pill variant="success" size="sm" v-on:click="detalle" class="mr-2">
          <b-icon icon="graph-up"></b-icon>Detalles
        </b-button>
        <b-button pill variant="success" size="sm" v-on:click="agregar" class="mr-2">
          <i class="ni ni-chart-bar-32"></i>
          Agregar
        </b-button>
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
//import json from "../../../../public/pruebas/cedears.json";

export default {
  data() {
    return {
      perPage: 15,
      currentPage: 1,
      sortBy: "id",
      sortDesc: false,
      keyword: "",
      fields: [
        //{ key: "id", sortable: true },
        //{ key: "assetType", sortable: false },
        { key: "ticker", label: "Nombre", sortable: true },
        { key: "description", label: "Descripcion", sortable: true },
        { key: "acciones", label: "", sortable: false },
      ],
      cedears: [],
    };
  },
  methods: {
    detalle() {
      console.log("Editar");
    },
    agregar() {
      console.log("Agregar");
    },
    getCedears() {
      const baseURI = "http://127.0.0.1:3010/api/asset/all";
      this.$http.get(baseURI).then((result) => {
        this.cedears = result.data;
      });
    },
  },
  computed: {
    rows() {
      return this.cedears.length;
    },
    items() {
      return this.keyword
        ? this.cedears.filter(
            (item) =>
              item.ticker.includes(this.keyword) ||
              item.description.includes(this.keyword)
          )
        : this.cedears;
    },
  },
  mounted() {
    this.getCedears();
  },
};
</script>
