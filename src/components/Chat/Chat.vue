<script setup>
    //import ref
    import { ref, onMounted, computed } from 'vue';

    let message = ref(''); //int, string, boolean
    let allMessages = ref({
        data: [],
    }); //array, object

    //API van Ismail binnenhalen
    onMounted(async () => {
        try {
            const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
            const data = await response.json();

            if (Array.isArray(data)) {
            allMessages.value.data = data.slice(0,20).map(message => ({
                username: message.user,
                message: message.text,
                //get a random rgb color
                color: `rgb(${Math.floor(Math.random() * 255)}, ${Math.floor(Math.random() * 255)}, ${Math.floor(Math.random() * 255)})`,
            }));
            console.log(allMessages.value.data);
            } else {
            console.error('Invalid API response:', data);
            }
        } catch (error) {
            console.error('Error fetching data:', error);
        }
    });

    //function sendMessage
    const sendMessage = () => {
        allMessages.value.data.push({
            username: "Me", 
            message: message.value,
            //get a random rgb color
            color: `rgb(0,128,0)`,
        });
        //clear input field
        message.value = '';
    };

    const reversedMessages = computed(() => allMessages.value.data.slice().reverse());
</script>

<template>
  <div>
    <div class="scrollable">
        <ul v-if="reversedMessages.length > 0">
            <li v-for="m in reversedMessages" :key="m._id">
                <div class="detailsHead">
                    <div class="userHead">
                        <div class="profileBanner">
                            <div class="profileImage" :style="{ backgroundColor: m.color }"></div>
                            <div class="messageText">
                                <h3>{{ m.username }}</h3>
                                <p>{{ m.message }}</p>
                            </div>
                        </div>
                        <a href="#" class="heart"></a>
                    </div>
                </div>
            </li>
        </ul>
        <p v-else>No messages available</p>
    </div>

    <div class="inputField">
        <div>
            <input v-model="message" type="text" placeholder="" />
            <button @click="sendMessage">Send</button>
        </div>
    </div>
  </div>
</template>

<style scoped>
    .scrollable {
        max-height: 480px;
        overflow-y: scroll;
    }
    ::-webkit-scrollbar {
        width: 10px;
    }
    ::-webkit-scrollbar-track {
        background: #f2f2f2;
        border-radius: 5px;
    }
    ::-webkit-scrollbar-thumb {
        background: #888;
        border-radius: 5px;
    }
    ul li {
        list-style-type: none;
        margin: 0;
        margin-bottom: 10px;
        padding-top: 20px;
        padding-bottom: 20px;
        width: 94%;
    }
    ul li:hover {
        background-color: #f2f2f2;
        border-radius: 10px;
    }
    .detailsHead {
    width: calc(92% - 20px);
    margin-left: 40px;
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
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #3EA055;
    margin-right: 12px;
    background-image: url('./src/assets/profile.png');
    background-size: 40%;
    background-position: center;
    background-repeat: no-repeat;
  }
  .messageText h3 {
    margin: 0;
  }
  .messageText p {
      margin: 0;
      font-size: 14px;
      color: #333333;
  }
  .heart {
    width: 30px;
    height: 30px;
    background-image: url('./src/assets/heart.png');
    background-size: 100%;
    background-position: center;
    background-repeat: no-repeat;
    margin-right: 20px;
  }
  .inputField {
    width: 33%;
    height: 60px;
    background-color: #f2f2f2;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    bottom: 0;
    right: 3px;
    border-top: 2px solid #e6e6e6;
  }
  input {
    width: 60%;
    height: 40px;
    border-radius: 20px 0 0 20px;
    border: none;
    padding-left: 20px;
    font-size: 16px;
  }
  button {
    width: 20%;
    height: 40px;
    border-radius: 0 20px 20px 0;
    border: none;
    background-color: #5d8dd6;
    color: white;
    font-size: 16px;
    font-weight: 600;
  }
  button:hover {
      cursor: pointer;
  }
</style>
