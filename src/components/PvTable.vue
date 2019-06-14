<template>
  <div>
    <div class="actions">
      <!-- Filters -->
      <pv-filters :filters="filtersData"/>

      <!-- Add filter component -->
      <pv-dropdown :options="fields" @option="addOptionToFilters"/>
    </div>

    <table class="table">
      <thead>
        <tr>
          <th v-for="(field, index) in fields" :key="index">{{ field }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in filteredItems" :key="index">
          <td v-for="(field, pos) in fields" :key="pos">{{ item[field] }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import PvFilters from "@/components/PvFilters";
import PvDropdown from "@/components/PvDropdown";
export default {
  name: "PvTable",
  components: {
    PvFilters,
    PvDropdown
  },
  props: {
    items: {
      type: Array,
      required: true
    },
    filters: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      fields: Object.keys(this.items[0]),
      rows: [],
      filtersData: this.filters,
      filteredItems: []
    };
  },

  mounted() {
    this.filteredItems = this.getItems();
  },

  methods: {
    addOptionToFilters(filter) {
      this.filtersData.push(filter);
      this.filtersData = [...new Set(this.filtersData)];
    },

    getItems() {
      let rows = {};
      let data = [];

      this.items.forEach(item => {
        for (let prop in item) {
          rows[prop] = item[prop];

          if (prop === "tags") {
            rows[prop] = String(item[prop]);
          }

          if (prop === "metrics") {
            let metricArr = [];
            item[prop].forEach((metric, ind) => {
              metricArr[ind] = Object.values(metric);
              rows[prop] += String([Object.values(metric)]);
            });
            rows[prop] = metricArr.toString();
          }
        }
        data.push(rows);
      });
      return data;
    }
  }
};
</script>

<style lang="scss" scoped>
.actions {
  display: flex;
  align-items: center;
  padding: 1.5rem 0;
}

.table {
  border-collapse: collapse;
  color: #202020;
  width: 100%;
}

.table thead th {
  color: #fff;
  background-color: #00a248;
  border-color: #007132;
  text-transform: capitalize;
}

.table th,
.table td {
  padding: 0.75rem;
  border-top: 1px solid #dee2e6;
  border-bottom: 1px solid #dee2e6;
}

.table tr:nth-child(odd) {
  background-color: #e6f5ed;
}

.table tr:nth-child(even) {
  background-color: #f5f8f7;
}
</style>