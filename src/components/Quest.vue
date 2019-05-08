<template>
    <li class="quest-item">
        <div class="status">
            <input type="checkbox" :checked="checked">
        </div>
        <div class="title">
            <textarea v-model="title" placeholder="Title"></textarea>
        </div>
        <svg preserveAspectRatio="none" viewBox="0 0 40 40" height="40px" width="40px">
            <polygon points="0,0 30,0 0,40" />
        </svg>
    </li>
</template>

<script>
    export default {
        name: "Quest",
        props: ['title','checked'],
        data() {
            return {

            }
        }
    }
</script>

<style scoped>
</style>