<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/playvox.svg">
    <pv-table :items="sourceData" :filters="filters"/>
  </div>
</template>

<script>
import sourceData from "@/data.json";
import PvTable from "./components/PvTable.vue";

export default {
  name: "app",
  components: {
    PvTable
  },

  data() {
    return {
      sourceData,
      filters: ["status"]
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
}
</style>
