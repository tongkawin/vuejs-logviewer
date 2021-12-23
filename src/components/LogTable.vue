<template>
  <div>
    <b-table stacked :items="items" content-class="mt-3">
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