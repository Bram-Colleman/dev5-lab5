<script setup>
import { ref, onMounted } from 'vue';

const comments = ref([]);
const comment = ref("");
const username = ref("");
onMounted(() => {
    fetchComments();
});

const fetchComments = async () => {
    const response = await fetch(`https://dev5-lab4-1hlz.onrender.com/api/v1/messages`);
    const res = await response.json();

    res.data.messages.forEach(message => {
        comments.value.push(message);
    });
};

const send = async () => {
    try {
        if (comment.value && username.value) {
            const response = await fetch('https://dev5-lab4-1hlz.onrender.com/api/v1/messages', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    message: {
                        user: username.value,
                        text: comment.value ,
                    }
                }),
            });
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            } else {
                const data = await response.json();
-               comments.value.push(data.data.message);
                comment.value = '';
            }
        }
    }
    catch (error) {
        console.error('An error occurred while posting the comment:', error);
    }
};

</script>
<template>
    <ul>
        <li v-for="comment in comments.slice().reverse()">
            <p><strong>{{ comment.user }}</strong></p>
            <p>{{ comment.text }}</p>
        </li>
    </ul>
    <div class="add">
        <input type="text" v-model="username" placeholder="Username" id="input--user">
        <input type="text" v-model="comment" placeholder="Add comment..." id="input--text">
        <button id="send" v-on:click="send">Send</button>
    </div>
</template>
<style scoped>
ul {
    height: 75vh;
    width: 50vw;
    list-style: none;
    overflow-y: scroll;
    background-color: #f8f8f8;
    margin: 0;
}
.add {
    height: 5vh;
    display: flex;
    flex-grow: 1;
}
#input--user {
    width: 10vw;
}
#input--text {
    width: 35vw;
}
button {
    width: 5vw;
    height: 5vh;
    display: flex;
    flex-grow: 1;
    align-self: center;
    justify-content: center;
    align-items: center;
}
p {
    margin: 0;
}
li {
    margin: 1rem;
}
</style>