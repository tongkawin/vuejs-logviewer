<template>
  <div class="search">
    <form @submit="handleInput()">
      <b-input-group prepend="Request UID" class="mt-3">
        <b-form-input
          v-model="value"
          :placeholder="placeholder"
          v-debounce="1500"
        ></b-form-input>
        <b-input-group-append>
          <b-button @click="handleInput()" variant="info">Search</b-button>
        </b-input-group-append>
      </b-input-group>
    </form>
  </div>
</template>

<script>
import debounce from "v-debounce";
export default {
  directives: {
    debounce,
  },
  props: {
    value: { default: "" },
    placeholder: { default: "Search" },
  },
  name: "Search",
  methods: {
    handleInput() {
      this.$emit("input", this.value);
    },
  },
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
