<template>
  <div class="filterTitle">
    <img src="../assets/arrowleft.svg" />
    <h2>All Time</h2>
    <img src="../assets/arrowrigtht.svg" />
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.filterTitle {
  display: flex;
  align-items: center;
  justify-content: center;
  img {
    height: 2rem;
  }
  h2 {
    font-size: 3rem;
    margin: 0px 15px;
  }
}
@media (max-width: 800px) and (max-width: 649px) {
  .filterTitle {
    margin-bottom: 10px;
    h2 {
      font-size: 2rem;
    }
  }
}
@media (max-width: 650px) {
  .filterTitle {
    align-self: center;
    margin-bottom: 20px;
  }
}
</style>
