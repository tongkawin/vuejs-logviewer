<template>
  <div>
    <b-table striped hover :items="items" @row-clicked="onRowSelected">
    </b-table>
  </div>
</template>

<script>
export default {
  props: {
    items: [],
  },
  data() {
    return {};
  },
  methods: {
    onRowSelected(item) {
      this.$emit("rowClick", item);
    },
  },
};
</script>