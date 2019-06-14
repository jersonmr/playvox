<template>
  <select class="filters">
    <option value v-for="(filter, index) in filters" :key="index">{{ filter }}</option>
  </select>
</template>

<script>
export default {
  props: {
    filters: {
      type: Array,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.filters {
  border: 1px solid #007132;
  font-size: 1rem;
  padding: 0.5rem 1rem;
}

.filters:focus {
  border: 1px solid #007132;
}
</style>