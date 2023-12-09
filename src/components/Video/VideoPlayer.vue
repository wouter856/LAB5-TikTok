<script setup>
    import { ref, reactive, onMounted } from 'vue';

    //define emits
    const emits = defineEmits(['update:videoURL']);
    
    const videoURL = ref("");
    let videos = reactive({
        data: [],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
            .then((res) => res.json())
            .then((data) => {
                console.log(data);
                videos.data = data.record.videos;
                videoURL.value = videos.data[0].video;

                emits('update:videoDescription', videos.data[0].description);
            });
    });
</script>

<template>
  <div>
    <video :src="videoURL" controls autoplay muted loop></video>
  </div>
</template>

<style scoped>

</style>
