<template>
  <div class="row d-flex justify-content-center">
    <div class="w-75">
      <br />
      <LogTable :items="logdata"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import LogTable from "@/components/LogTable.vue";
export default {

  components: {
    LogTable
  },
  data() {
    return {
      logdata: []
    };
  },
  mounted() {
    const LogID = (this.$route.params).logid;
    const url = `http://localhost:3000/search-LogID/${LogID}`
    axios
      .get(url)
      .then(({ data }) => {
        const response = data.hits.hits;
        this.logdata = response.map((i) => {
            console.log(i);
            return i._source.Source
          });
      });
  },
  methods: {
    countDownChanged(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },
    showAlert() {
      this.dismissCountDown = this.dismissSecs;
    },
  },
};
</script>