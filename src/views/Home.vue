<template>
  <div class="row d-flex justify-content-center">
    <div class="w-75">
      <h1>API Log Viewer</h1>
      <b-alert v-if="error" show variant="danger">{{ error }}</b-alert>
      <Search v-model="searchInput" />
      <br />
      <Table class="table-bordered" :items="log" @rowClick="rowClick"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "@/components/Search.vue";
import Table from "@/components/Table.vue";
export default {
  name: "Home",
  components: {
    Search,
    Table,
  },
  data() {
    return {
      searchInput: "",
      log: [],
      error: false,
    };
  },
  methods: {
    rowClick(item) {
      const { RequestUID, LogID } = item;
      this.$router.push(`/${RequestUID}/${LogID}`);
    },
    getData(key) {
      this.log = [];
      this.error = null;
      const url = `http://localhost:3000/search-requestUid/${key}`
      axios
        .get(url)
        .then(({ data }) => {
          const responseData = data.hits.hits;
          this.log = responseData.map((i) => {
            console.log(i);
            return {
              RequestUID: i._source.RequestUid,
              ApplicationName: i._source.Source.applicationName,
              gwLatency: i._source.Source.gwLatency,
              timestamp: i._source.Source['@timestamp'],
              LogID: i._id,
            };
          });
        })
        .catch(() => {
          this.error = `No result`;
        });
    },
  },
  mounted() {
    const { requid } = this.$route.params;
    if (requid) {
      this.getData(requid);
      this.searchInput = requid;
    }
  },
  watch: {
    searchInput(input) {
      const { requid } = this.$route.params;
      if (requid != input) this.$router.push(`/${input}`);
    },
    $route() {
      const { requid } = this.$route.params;
      if (requid) {
        this.getData(requid);
        this.searchInput = requid;
      }
    },
  },
};
</script>
