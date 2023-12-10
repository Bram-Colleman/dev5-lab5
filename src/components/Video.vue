<script setup>
import { ref } from 'vue';
import Commentsection from './Commentsection.vue';

let videoUrl = ref("https://vue-3-tiktok.vercel.app/video1.mp4");

</script>
<template>
    <div class="container">
        <div class="container--video">
            <video :src="videoUrl" controls autoplay muted></video>
        </div>
        <div class="details">
            <div class="details--video">
                <h3>Sami2bx</h3>
                <p>No space on metro? 🦄</p>
            </div>
            <Commentsection></Commentsection>
        </div>
    </div>
</template>
<style scoped>
.container {
  display: flex;
  align-items: center;
}
.container--video {
    display: flex;
    flex-direction: column;
    align-self: center;
    justify-content: center;
}
video {
    height: 90vh;
    width: fit-content !important;
}
.details {
    height: 90vh;
}
.details--video {
    height: 10vh;
    padding-left: 2rem;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 0rem 2rem;
}
h3, p {
    margin: 0;
}
</style>