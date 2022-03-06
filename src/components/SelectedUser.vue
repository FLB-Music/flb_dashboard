<template>
  <div class="selected_user">
  <p class="user_id">{{selectedUserDetails.id}}</p>
  <div class="main_info">
   <div class="launches_wrapper">
     <p>{{selectedUserDetails.numberOfLaunches}}</p>
     <p>Opens</p>
   </div>
   <div class="os_logo">
      <img v-if="selectedUserDetails.os_type=='Linux'" src="@/assets/linux.png" alt="">
      <img v-if="selectedUserDetails.os_type=='Windows_NT'" src="@/assets/windows.png" alt="">
      <img v-if="selectedUserDetails.os_type=='Darwin'" src="@/assets/mac.png" alt="">
   </div>
   <div> 
      <p>4/8 gb</p>
      <p>Free</p>
   </div>
   <div> 
      <p>{{selectedUserDetails.cpu_no}}</p>
      <p>Cores</p>
   </div>
  </div>
  
  <div class="launches">
    <p class="h">Launches</p>
    <div>
     <p v-for="launch in selectedUserDetails.app_launches" :key="launch" >{{launch.substr(0,25)}}</p>
    </div>
  </div>

 </div>
</template>

<script>
export default {
props:{
    selectedUserDetails: Object
  }
}
</script>

<style scoped lang="scss">
.selected_user{
    width: 30vw;
    padding: 10px;
  }
.user_id{
    text-align: center;
    width: 100%;
    font-size: 2rem;
    font-weight: 300;
    margin-bottom: 10px;
  }
p{
  font-weight: 300;
}
.launches{
  margin-top: 20px;
  border: 1px solid grey;
  border-bottom: none;
  height: 71vh;
  overflow: hidden;
  overflow-y: scroll;
  .h{
        text-align: center;
        font-size: 1.5rem;
        border-bottom: 1px solid grey;
  }
  div {
    p{
        border-bottom: 1px solid grey;
        text-align: center;
      }
    }
  }
.main_info{
    display: flex;
    justify-content: space-between;
    div{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    p{
        font-size: 1.5rem;
      }
  }
img{
    filter: grayscale(1);
    width: 2.2rem;
  }
</style>
