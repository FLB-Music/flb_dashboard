<template>
  <div id="app">
    <div class="flex align_start">
      <div class="mr10">
        <div class="sub_fil flex justify_between align_start pa10">
          <sub-totals />
          <filter-title />
        </div>
        <stats-table class="ma10" />
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
  components: {
    SubTotals,
    StatsTable,
    FilterTitle,
    Filters
  }
};
</script>

<style lang="scss">
@import url("./assets/styles/global.css");
#app {
  background: white;
  height: 100%;
  padding: 20px;
}
@media (max-width: 800px) and (max-width: 650px) {
  .sub_fil {
    flex-direction: column-reverse;
  }
}
</style>
