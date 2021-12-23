<template>
  <div>
    <b-table :items="items" small bordered striped no-border-collapse responsive>
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