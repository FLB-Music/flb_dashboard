<template>
  <div id="app">
    <login
      v-if="!isLoggedIn"
      leave-active-class="animate faster slideOutDown"
      :msg="adminResponse.error"
      v-on:adminKey="key => (ADMIN_KEY = key)"
    />
    <div class="paper_wrap" v-if="distribution">
      <div class="wrapper">
       <distribution :distribution="distribution" /> 
      </div>
    </div>

    <div class="paper_wrap">
      <div class="wrapper flex align_start">
        <div class="wrapper m10">
          <div class="sub_fil flex justify_between align_start pa10">
            <sub-totals :stats="stats" />
            <filter-title />
          </div>
          <stats-table v-if="stats" @selectUser="setSelectedUser" :stats="stats" class="ma10" />
        </div>
        <filters />
      </div>
    </div>

    <div class="paper_wrap" v-if="selectedUserDetails">
      <div class="wrapper">
        <selected-user :selectedUserDetails='selectedUserDetails'/>
      </div>
    </div>


  </div>
</template>

<script>
import SubTotals from "./components/SubTotals.vue";
import StatsTable from "./components/StatsTable.vue";
import FilterTitle from "./components/FilterTitle.vue";
import Filters from "./components/Filters.vue";
import SelectedUser from "./components/SelectedUser.vue";
import Distribution from "./components/Distribution.vue";
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
      },
      selectedUserDetails: null,
      distribution: null
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
    Login,
    SelectedUser,
    Distribution
  },
  methods: {
    setSelectedUser(data){
      this.selectedUserDetails = data;
     },
    async getStats() {
      const response = await fetch(
        `https://flb-server.herokuapp.com/get-stats?adminKey=${this.ADMIN_KEY}`
      );
      if (response.status == 200) {
        this.stats = await response.json();
        const timezoneReg = /\(.*\)/gm
        this.stats.map(stat=>{
         const matches = stat.app_launches[0].match(timezoneReg)
          stat['timezone'] = matches[0].replace('(','').replace(')','')
          stat['numberOfLaunches'] = stat.app_launches.length
          stat['installDate'] = new Date(stat.app_launches[0])
          stat['lastLaunch'] = new Date(stat.app_launches[stat.app_launches.length -1])
          })
        this.isLoggedIn = true;
        localStorage.setItem("adminKey", this.ADMIN_KEY);
      console.log(this.stats);
        this.getDistribution()
      } else {
        this.adminResponse = await response.json();
        console.log(this.adminResponse);
      }
    },
    getDistribution(){
      const linux = this.stats.filter(stat=>stat.os_type=="Linux").length
      const mac = this.stats.filter(stat=>stat.os_type=="Darwin").length
      const win = this.stats.filter(stat=>stat.os_type=="Windows_NT").length
      this.distribution = {
       linux,
       mac,
       win
      }
      console.log(linux)
      console.log(win)
      console.log(mac)
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
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  padding: 20px;
} 
.paper_wrap{
  height: 97vh;
    background: grey;
    padding-bottom: 1px;
    padding-right: 1px;
  }
.wrapper {
  background: white;
  height: 100%;
  padding: 10px;
  display: flex;
  flex-direction: column;
}
@media (max-width: 800px) and (max-width: 650px) {
  .sub_fil {
    flex-direction: column-reverse;
  }
}
</style>
