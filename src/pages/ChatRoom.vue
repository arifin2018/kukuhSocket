<script setup>
    import ListChat from '../components/chats/ListChat.vue'
    import RoomChat from '../components/chats/RoomChat.vue'
</script>

<template>
    <section class="flex flex-row h-screen">
        <h1 class="basis-1/4 h-full border-r-2 border-black">
            <ListChat/>
        </h1>
        <h1 class="h-full w-screen">
            <RoomChat/>
        </h1>
    </section>
</template>

<style>
</style>