<template>
  <div class="subtotals">
    <div class="sub">
      <div class="circle"></div>
      <h3>{{ stats.length }} Users</h3>
    </div>
    <div class="sub">
      <div class="circle no-line"></div>
      <h3>
        {{
          stats
            .map(stat => stat.app_launches.length)
            .reduce((acc, val) => acc + val, 0)
        }}
        Launches
      </h3>
    </div>
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
.subtotals {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  .sub {
    display: flex;
    align-items: center;
    justify-content: center;
    h3 {
      font-size: 3rem;
    }
    .circle {
      position: relative;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      border: 1px solid black;
      margin-right: 10px;
      background: white;
      &:after {
        content: "";
        position: absolute;
        left: 50%;
        bottom: 0%;
        transform: translate(-50%, 100%);
        width: 1px;
        background: black;
        height: 3rem;
      }
    }
    .no-line:after {
      display: none;
    }
  }
}
@media screen and (max-width: 800px) {
  .subtotals {
    .sub {
      h3 {
        font-size: 2rem;
      }
      .circle:after {
        height: 2rem;
      }
    }
  }
}
</style>
