<script>
    import ListChat from '../components/chats/ListChat.vue'
    import RoomChat from '../components/chats/RoomChat.vue'
    import Login from '../components/Login.vue'
    import socket from '../helpers/socket.js'
    
    export default {
        data() {
            return {
                name:"",
                isRegistered: false,
                availableUser:[],
                activeConversation: null,
                messageRoom: "",
                conversation: {},
                text:""
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
            },
            onClickUser(user){
                let raw = localStorage.getItem("userChat")
                this.activeConversation = user
                console.log("this.activeConversation");
                console.log(this.activeConversation);
                if (raw) {
                    const me = JSON.parse(raw)
                    let room = [
                        user.id, me.id
                    ].sort().join("&")
                    this.messageRoom = room
                    if (this.conversation["room"]) {
                        this.conversation["room"] = this.conversation["room"].map(item => {
                            return {
                                ...item,
                                read: true
                            } 
                        }) 
                    }
                }
                /**
                 * windows 1
                 * {
                 * "nama":"awd",
                 * "room":"awdad-1213",
                 * "read":true
                 * },
                 * {
                 * "nama":"awd2",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * {
                 * "nama":"awd3",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * 
                 * windows 2
                 * {
                 * "nama":"awd",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * {
                 * "nama":"awd2",
                 * "room":"awdad-1213",
                 * "read":true
                 * },
                 * {
                 * "nama":"awd3",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * 
                 * windows 3
                 * {
                 * "nama":"awd",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * {
                 * "nama":"awd2",
                 * "room":"awdad-1213",
                 * "read":false
                 * },
                 * {
                 * "nama":"awd3",
                 * "room":"awdad-1213",
                 * "read":true
                 * },
                 * 
                 * 
                 */
            },
            onSendMessage(){
                if (this.text) {
                    let raw = localStorage.getItem("userChat")
                    if (raw) {
                        const me = JSON.parse(raw)
                        socket.emit('PRIVATE_MESSAGE', {
                            from: me,
                            to: this.activeConversation,
                            date: new Date(),
                            text: this.text,
                            read: false,
                            room: [
                                this.activeConversation.id, me.id
                            ].sort().join("&")
                        });
                        this.text = ""
                    }
                }
            },
            onChangeText(e){
                this.text = e.target.value
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
                let raw = localStorage.getItem("userChat")
                if (raw) {
                    const me = JSON.parse(raw)
                    this.availableUser = data.filter(user => {
                        console.log("user");
                        console.log(user);
                        return user.id !== me.id 
                    })
                }
            })
            
            let dataUser = localStorage.getItem("userChat")
            if (dataUser) {
                socket.emit('RECONNECT', JSON.parse(dataUser))
                this.isRegistered = true
            }
            socket.on("PRIVATE_MESSAGE",data => {
                console.log("data" + data.from.id + "   conver id" + this.activeConversation.id );
                console.log(data);

                const fromActive = this.activeConversation.id === data.from.id
                const dataWithStatusUpdate = fromActive ? {
                    ...data,
                    read: true
                } : data
                if (this.conversation[data.room]) {
                    this.conversation[data.room].push(dataWithStatusUpdate)
                }else{
                    this.conversation[data.room] = [dataWithStatusUpdate]
                }
                console.log("this.conversation");
                console.log(this.conversation);
            })
        },
    }
</script>

<template>
    <Login v-if="!isRegistered" :name="name" :onChange="inputName" :isRegistered="isRegistered" @dataIsRegistered="dataIsRegistered"></Login>
    <section v-else class="flex flex-row h-screen">
        <h1 class="basis-1/4 h-full border-r-2 border-black">
            <ListChat :availableUser="availableUser" :onClickUser="onClickUser"/>
        </h1>
        <h1 class="h-full w-screen" v-if="activeConversation">
            <RoomChat :onSendMessage="onSendMessage" :onChangeText="onChangeText" :conversation="conversation" :messageRooms="messageRoom" :text="text"/>
        </h1>
    </section>
</template>

<style>
</style>