<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue';

// Define emits
const emits = defineEmits(['update:videoDescription', 'update:videoUsername']);

const videoURL = ref("");
const currentIndex = ref(0); // Initial index

let videos = reactive({
    data: [],
});

//change index of video array when using arrow up or down
const changeIndex = (newIndex) => {
    if (newIndex >= 0 && newIndex < videos.data.length) {
        currentIndex.value = newIndex;
        updateVideo();
    }
};

const updateVideo = () => {
    videoURL.value = videos.data[currentIndex.value].video;
    emits('update:videoDescription', videos.data[currentIndex.value].description);
    emits('update:videoUsername', videos.data[currentIndex.value].username);
};

const handleKeyDown = (event) => {
    if (event.key === 'ArrowUp') {
        changeIndex(currentIndex.value - 1);
    } else if (event.key === 'ArrowDown') {
        changeIndex(currentIndex.value + 1);
    }
};

onMounted(() => {
    fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
        .then((res) => res.json())
        .then((data) => {
            console.log(data);
            videos.data = data.record.videos;
            updateVideo();
        });
    window.addEventListener('keydown', handleKeyDown);
});

onBeforeUnmount(() => {
    window.removeEventListener('keydown', handleKeyDown);
});
</script>

<template>
  <div>
    <video :src="videoURL" controls autoplay muted loop></video>
  </div>
</template>

<style scoped>
  video {
    width: 400px;
    height: auto;
  }
</style>
