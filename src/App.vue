<template>
  <div id="app">
    <login
      v-if="!isLoggedIn"
      leave-active-class="animate faster slideOutDown"
      :msg="adminResponse.error"
      v-on:adminKey="key => (ADMIN_KEY = key)"
    />
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
import Login from "./components/Login.vue";
export default {
  name: "App",
  data() {
    return {
      ADMIN_KEY: "null",
      adminResponse: "",
      isLoggedIn: false,
      stats: [],
      subTotals: {
        currentFilterUsers: 0,
        lifeTimeUsers: 0,
        currentFilterLaunches: 0
      }
    };
  },
  watch: {
    ADMIN_KEY() {
      console.log("Admin Key Changed");
      this.getStats();
    }
  },
  components: {
    SubTotals,
    StatsTable,
    FilterTitle,
    Filters,
    Login
  },
  methods: {
    async getStats() {
      console.log("OOhhh yeea");
      const response = await fetch(
        `https://flb-server.herokuapp.com/get-stats?adminKey=${this.ADMIN_KEY}`
      );
      console.log(response);
      if (response.status == 200) {
        this.stats = await response.json();
        this.isLoggedIn = true;
        localStorage.setItem("adminKey", this.ADMIN_KEY);
      } else {
        this.adminResponse = await response.json();
        console.log(this.adminResponse);
      }
    }
  },
  mounted() {
    const key = localStorage.getItem("adminKey");
    if (key) {
      this.ADMIN_KEY = key;
      this.getStats();
    }
  }
};
</script>

<style lang="scss">
@import url("./assets/styles/global.css");
@import url("./assets/styles/animate.css");
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
