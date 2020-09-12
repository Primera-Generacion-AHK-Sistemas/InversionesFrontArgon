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
    ></b-table>

    <b-card-footer class="py-4">
      <div>

        <b-pagination
          v-model="currentPage"
          pills
          size="sm"
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
import json from "../../../../public/response.json"

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
        { key: "ticker", sortable: true },
        { key: "description", sortable: true },
      ],
      items: json,
    };
  },
  computed: {
    rows() {
      return this.items.length;
    },
  },
};
</script>
