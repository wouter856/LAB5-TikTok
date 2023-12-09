<script setup>
  //define properties
  const props = defineProps(['description', 'username']);
</script>

<template>
  <div class="detailsHead">
    <div class="userHead">
      <div class="profileBanner">
        <div class="profileImage"></div>
        <h3>{{ username }}</h3>
      </div>
      <a href="#">Follow</a>
    </div>
    <p>{{ description }} <span>#Vomit</span> <span> #BXL</span> <span> #Funny</span></p>
  </div>
</template>

<style scoped>
  .detailsHead {
    padding: 10px;
    width: calc(92% - 20px);
    margin-top: 20px;
    margin-bottom: 40px;
    margin-left: 4%;
    background-color: #f2f2f2;
    border-radius: 10px;
  }
  .userHead {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .profileBanner {
    display: flex;
    align-items: center;
  }
  .profileImage {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: #3EA055;
    margin-right: 12px;
    background-image: url('./src/assets/profile.png');
    background-size: 40%;
    background-position: center;
    background-repeat: no-repeat;
  }
  span {
    font-weight: 600;
    color: #0437f0;
    margin-left: 10px;
  }
  span:hover {
    color: #00308F;
    cursor: pointer;
  }
</style>
