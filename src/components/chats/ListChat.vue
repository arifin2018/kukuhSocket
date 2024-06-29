<script>
    export default{
        props:{
            availableUser: Array,
            onClickUser: Function
        },
        data() {
            return {
                
            }
        }, 
    }
</script>

<template>
    <div class="flex flex-col">
        <div class="bg-cyan-400 p-3 border-b-2 border-black" v-for="user in availableUser" :key="user.id" @click="onClickUser(user)">
            <div class="flex justify-between">
                <span>{{ user.name }}</span>
                <span class="text-green-300">{{ user.isActive ? "online" :"offline" }}</span>
            </div>
        </div>
    </div>
</template>

<style>
</style>