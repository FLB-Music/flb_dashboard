<template>
  <div class="distribution">
    <div class="byOs">
      <div class="os">
        <img src="@/assets/linux.png" alt="">
        <h3>{{distribution.linux}}</h3>
      </div>
      <div class="os">
        <img src="@/assets/windows.png" alt="">
        <h3>{{distribution.win}}</h3>
      </div>
      <div class="os">
        <img src="@/assets/mac.png" alt="">
        <h3>{{distribution.mac}}</h3>
      </div>

    </div>
  </div>
</template>

<script>
export default {
props:{
    distribution: Object
  }
}
</script>

<style lang="scss">
.byOs{
    display: flex;
    align-items: center;
    justify-content: center;
    gap:10px;
}
.os{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap:10;
  h3{
   font-size: 3rem;
  }
  img{
    height: 40px;
    filter: grayscale(1);
  }
  }

</style>
