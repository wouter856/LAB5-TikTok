<script setup>
  import VideoPlayer from './components/Video/VideoPlayer.vue';
  import VideoDetails from './components/Video/VideoDetails.vue';
  import Chat from './components/Chat/Chat.vue';
  
  import { ref } from 'vue';
  let newDescription = ref('');
  let newUsername = ref('');

  //listen for emits
  const updateVideo = (description) => {
    newDescription.value = description;

    if (description === 'No space on Metro? 🦄') {
      document.querySelector('.video').classList.remove('random');
      document.querySelector('.video').classList.remove('none');
      document.querySelector('.video').classList.add('sami');
    } else if (description === 'Burger Disco Duty') {
      document.querySelector('.video').classList.remove('sami');
      document.querySelector('.video').classList.remove('none');
      document.querySelector('.video').classList.add('random');
    } else {
      document.querySelector('.video').classList.remove('sami');
      document.querySelector('.video').classList.remove('random');
      document.querySelector('.video').classList.add('none');
    }
  };

  const updateUsername = (username) => {
    newUsername.value = username;
  };
</script>

<template>
  <div class="tiktok">
    <div class="video">
      <VideoPlayer @update:video-description="updateVideo" @update:video-username="updateUsername" />
    </div>
    <div class="side">
      <VideoDetails :description="newDescription" :username="newUsername" />
      <Chat />
    </div>
  </div>
</template>

<style scoped>
  .tiktok {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
  .video {
    display: flex;
    justify-content: center;
    height: 100%;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-color: #000000;
  }
  .video.sami {
    background-image: url('./assets/sami.jpg');
  }
  .video.random {
    background-image: url('./assets/random.jpg');
  }
  .video.none {
    background-image: none;
  }
  .side {
    background-color: #f2f2f2;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>
