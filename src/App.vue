<template>
  <div id="app">
    <div class="wrapper flex align_start">
      <div class="wrapper m10">
        <div class="sub_fil flex justify_between align_start pa10">
          <sub-totals :stats="stats" />
          <filter-title />
        </div>
        <stats-table :stats="stats" class="ma10" />
      </div>
      <filters />
    </div>
  </div>
</template>

<script>
import SubTotals from "./components/SubTotals.vue";
import StatsTable from "./components/StatsTable.vue";
import FilterTitle from "./components/FilterTitle.vue";
import Filters from "./components/Filters.vue";
export default {
  name: "App",
  data() {
    return {
      stats: [],
      subTotals: {
        currentFilterUsers: 0,
        lifeTimeUsers: 0,
        currentFilterLaunches: 0
      }
    };
  },
  components: {
    SubTotals,
    StatsTable,
    FilterTitle,
    Filters
  },
  methods: {
    async getStats() {
      console.log("OOhhh yeea");
      const response = await fetch(
        "https://flb-server.herokuapp.com/get-stats?adminKey=FLBTOTHEMOON"
      );
      this.stats = await response.json();
      console.log(this.stats);
    }
  },
  mounted() {
    this.getStats();
  }
};
</script>

<style lang="scss">
@import url("./assets/styles/global.css");
#app {
  background: white;
  height: 100vh;
  padding: 20px;
}
.wrapper {
  height: 100%;
}
@media (max-width: 800px) and (max-width: 650px) {
  .sub_fil {
    flex-direction: column-reverse;
  }
}
</style>
