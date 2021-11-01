<template>
  <div class="StatsTable">
    <table class="for_desktop">
      <tr>
        <th>User ID</th>
        <th>Launches</th>
        <th>Operatin System</th>
        <th>Time Zone</th>
      </tr>
      <tr v-for="userStat in stats" :key="userStat.id">
        <td>{{ userStat.id }}</td>
        <td>{{ userStat.app_launches.length }}</td>
        <td>{{ userStat.os_type }}</td>
        <td>{{ userStat.app_launches[0] }}</td>
      </tr>
    </table>

    <table class="for_mobile">
      <tr>
        <th>User ID</th>
        <th>Launches</th>
      </tr>
      <tr v-for="userStat in stats" :key="userStat.id">
        <td>{{ userStat.id }}</td>
        <td>{{ userStat.app_launches.length }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    stats: Array
  }
};
</script>

<style lang="scss">
.StatsTable {
  height: 62%;
  overflow: hidden;
  overflow-y: scroll;
}
table,
th,
td {
  border: 2px solid black;
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
      border: 2px solid white;
    }
  }
}
.for_mobile {
  display: none;
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
