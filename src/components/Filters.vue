<template>
  <div :class="[showFilter ? 'showFilter' : '', 'filters']">
    <div class="filter_toggles">
      <img
        v-if="!showFilter"
        @click="toggleFilter"
        src="../assets/open filter.svg"
        alt="open filter"
      />
      <img
        v-if="showFilter"
        @click="toggleFilter"
        src="../assets/close.svg"
        alt="close filter"
      />
    </div>
    <h4>Today</h4>
    <h4>Yesterday</h4>
    <h4>This Week</h4>
    <h4>This Month</h4>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showFilter: false
    };
  },
  methods: {
    toggleFilter() {
      this.showFilter = !this.showFilter;
    }
  }
};
</script>

<style lang="scss">
.filters {
  height: 100%;
  border: 2px solid black;
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: white;
  display: none;
  h4 {
    border: 2px solid black;
    padding: 10px;
    font-size: 1.5rem;
    margin: 10px;
    text-align: center;
    letter-spacing: 0.1rem;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    &:hover {
      filter: invert(1);
    }
  }
  .filter_toggles {
    background: white;
    display: none;
    padding: 2px;
    border-radius: 10px;
    cursor: pointer;
  }
}

@media (max-width: 800px) and (max-width: 600px) {
  .filters {
    display: grid;
    grid-template-columns: 1fr 1fr;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: auto;
    position: absolute;
    right: 20px;
    overflow-y: scroll;
    h4 {
      font-size: 1.5rem;
      margin: 5px;
      padding: 5px;
    }
  }
}
@media screen and (max-width: 650px) {
  .showFilter {
    transform: translateX(-50%) translateY(0%) !important;
  }
  .filters {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    left: 50%;
    bottom: 0px;
    transform: translateX(-50%) translateY(100%);
    width: 95%;
    border: 1px solid black;
    overflow: visible;
    h4 {
      font-size: 0.8rem;
      border: 1px solid black;
    }
    .filter_toggles {
      display: block;
      position: absolute;
      left: 45%;
      top: -50px;
      /* transform: translate(-50%, 0%); */
      img {
        width: 30px;
      }
    }
  }
}
</style>
