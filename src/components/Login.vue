<template>
  <div class="login_wrapper">
    <div class="login">
      <p>Enter Admin Password</p>
      <input
        v-model="key"
        placeholder="Poor Security all the way"
        type="password"
      />
      <p>{{ msg }}</p>
      <button @click="$emit('adminKey', key)">LOGIN</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      key: ""
    };
  },
  props: {
    msg: String
  }
};
</script>

<style lang="scss">
.login_wrapper {
  position: fixed;
  z-index: 3;
  width: 98.5vw;
  height: 97vh;
  top: 0px;
  left: 0px;
  margin: 10px;
  background: white;
  border: 2px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  .login {
    width: 300px;
    padding: 10px;
    border: 2px solid black;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }
}
</style>
