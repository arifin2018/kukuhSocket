<script>
    import ListChat from '../components/chats/ListChat.vue'
    import RoomChat from '../components/chats/RoomChat.vue'
    import Login from '../components/Login.vue'
    import socket from '../helpers/socket.js'
    
    export default {
        data() {
            return {
                name:"",
                isRegistered: false
            }
        },
        components: {
            ListChat,
            RoomChat,
            Login
        },
        methods: {
            inputName(value){
                this.name = value
            },
            dataIsRegistered(value){
                this.isRegistered = value
                //EMIT=KIRIM KE BACKEND
                socket.emit("JOIN",this.name)
            }
        },
        mounted() {
            // ON=NERIMA DARI BACKEND
            socket.on("AUTHORIZE", (data) => {
                console.log("Adw");
                localStorage.setItem("userChat", JSON.stringify(data));
            });
            socket.on("AVAILABLE_USER",(data)=>{
                console.log("tokai");
                console.log(data);
            })
            
            let dataUser = localStorage.getItem("userChat")
            if (dataUser) {
                socket.emit('RECONNECT', JSON.parse(dataUser))
                this.isRegistered = true
            }
        }
    }
</script>

<template>
    <Login v-if="!isRegistered" :name="name" :onChange="inputName" :isRegistered="isRegistered" @dataIsRegistered="dataIsRegistered"></Login>
    <section v-else class="flex flex-row h-screen">
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