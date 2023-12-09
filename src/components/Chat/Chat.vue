<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';

    let message = ref(''); //int, string, boolean
    let allMessages = reactive({
        data: [
        { username: "Bert", message: "Heel" },
        { username: "Jan", message: "even" },
        { username: "Dirk", message: "simpel" },
        { username: "Tom", message: "doen" }
        ],
    }); //array, object

    //function sendMessage
    const sendMessage = () => {
        allMessages.data.push(message.value);
        message.value = '';
    };
</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data"><h3>{{ m.username }}</h3><p>{{ m.message }}</p></li>
    </ul>

    <div>
        <input v-model="message" type="text" placeholder="" />
        <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<style scoped>
    ul li {
        list-style-type: none;
    }
</style>
