<template>
  <div class="StatsTable">
    <table class="for_desktop">
      <tr>
        <th>User ID</th>
        <th>Launches</th>
        <th>Operatin System</th>
        <th>Time Zone</th>
      </tr>
      <tr>
        <td>1750Medion</td>
        <td>1</td>
        <td>Windows NT</td>
        <td>GMT+0200 (Central European Summer Time)</td>
      </tr>
      <tr>
        <td>24726anythingyoucantypeUs</td>
        <td>3</td>
        <td>Linux</td>
        <td>GMT-0700 (Pacific Daylight Time)</td>
      </tr>
    </table>

    <table class="for_mobile">
      <tr>
        <th>User ID</th>
        <th>Launches</th>
      </tr>
      <tr>
        <td>1750Medion</td>
        <td>1</td>
      </tr>
      <tr>
        <td>24726anythingyoucantypeUs</td>
        <td>3</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
table,
th,
td {
  border: 2px solid black;
  border-collapse: collapse;
  padding: 5px;
  font-weight: 300;
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
