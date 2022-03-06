<template>
  <div class="StatsTable">
    <table class="for_desktop">
      <tr id="table_heading">
        <th @click="sort('id')">User ID</th>
        <th @click="sort('numberOfLaunches')">Launches</th>
        <th @click="sort('os_type')">Operatin System</th>
        <th @click="sort('timezone')">Time Zone</th>
      </tr>
      <tr @click="showDetails(userStat)" v-for="userStat in sortedStats" :key="userStat.id">
        <td>{{ userStat.id }}</td>
        <td>{{ userStat.app_launches.length }}</td>
        <td>{{ userStat.os_type }}</td>
        <td>{{ userStat.timezone }}</td>
      </tr>
    </table>

    <table class="for_mobile">
      <tr>
        <th>User ID</th>
        <th>Launches</th>
      </tr>
      <tr v-for="userStat in stats" :key="userStat.id">
        <td>{{ userStat.id }}</td>
        <td>{{ userStat.numberOfLaunches}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    stats: Array
  },
  data(){return{
      sortField:'numberOfLaunches',
      reverse: false
    }},
  computed:{
    sortedStats(){
        let statsToSort = this.stats
        const compare = (a,b) => {
          if (a[`${this.sortField}`] < b[`${this.sortField}`]) {
            return -1;
          }
          if (a[`${this.sortField}`] > b[`${this.sortField}`]) {
            return 1;
          }
          return 0;
        }
      statsToSort.sort(compare);
      if(this.reverse){
        return statsToSort.reverse()
      }else{
        return statsToSort
      }
     }
  },
  methods:{
    sort(sortField){
      if(this.sortField === sortField){
         this.reverse = true
      }else{
         this.sortField = sortField
      }
     },
    showDetails(data){
      this.$emit("selectUser", data);
      console.log(data)
     }   
  }
};
</script>

<style lang="scss">
.StatsTable {
  overflow: hidden;
  overflow-y: scroll;
  height: 74%;
}
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
  padding: 5px;
  font-weight: 300;
}
tr {
  background: white;
  cursor: pointer;
  &:hover {
    filter: invert(1);
    td {
      border: 1px solid white;
    }
  }
}
.for_mobile {
  display: none;
  position: relative;
}
  #table_heading{
    border: 1px solid black;
    background: white;
    position: sticky;
    top: 0px;
    box-shadow: 0px 4px 10px grey;
    z-index: 3;
    th{
    padding: 10px;
     font-weight: 900;      
     &:hover{
        background: black;
        color: white;
      }
    }
  }

@media screen and (max-width: 650px) {
  .for_mobile {
    display: block;
  }
  .for_desktop {
    display: none;
  }
  table,
  th,
  td {
    border: 1px solid black;
  }
}
</style>
