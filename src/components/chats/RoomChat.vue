<template>
    <header class="border-b-2 border-black pb-2 p-3">
        Chat from {{ interculoterId }}
    </header>
    <div class="flex flex-col w-full relative h-[95%]">
        <div class="absolute overflow-y-auto max-h-full w-full flex flex-col">
            <div :class="[
                'my-3 mx-2 max-w-full text-right',
                isSelf(conversatio.from.id) ? 'justify-end' : 'justify-start'
            ]"  v-for="(conversatio,index) in conversation[messageRooms] || []" :key="index">
                <div :class="[
                    'max-w-6xl px-3 pt-2 rounded-lg',
                    isSelf(conversatio.from.id) ? 'float-end bg-[#37bb4f] ' : 'float-start bg-[#a7a7aa]'
                ]">
                    <div>{{ conversatio.text }}</div>
                    <div class="flex text-right float-end">
                        <p class="text-gray-600 text-sm p-1">08:00</p>
                        <box-icon color="blue" name='check-double'></box-icon>
                    </div>
                </div>
            </div>
            <div class="my-3 mx-2 max-w-full text-left justify-start">
                
            </div>
        </div>
    </div>
    <footer class="w-full relative">
        <div class="absolute">
            <input type="text" name="Arifin" id="Arifin" :value="text" class="w-full fixed bottom-0 h-12 border-t-2 border-black" @keyup.enter="onSendMessage" @input="onChangeText">
        </div>
    </footer>
</template>

<script>
    import 'boxicons'

    export default{
        props:{
            onSendMessage: Function,
            onChangeText: Function,
            conversation: Object,
            messageRooms: String,
            text: String
        },
        data() {
            return {
                meId:"",
                interculoterId: ""
            }
        },
        computed: {
            isSelf: function(){
                return (id) => {
                    let raw = localStorage.getItem("userChat")
                    if (raw) {
                        const me = JSON.parse(raw)
                        return me.id === id 
                    }
                }
            },
        },
        methods: {
            splitDataMessageRoom(dataMessageRooms){
                console.log(dataMessageRooms);
                const myArray = dataMessageRooms.split("&");
                this.meId = myArray[1]
                this.interculoterId = myArray[0] 
            }
        },
        mounted() {
            this.splitDataMessageRoom(this.messageRooms)
        },
        watch:{
            messageRooms: function(newVal, oldVal) { // watch it
                this.splitDataMessageRoom(newVal)
            }
        }
    }
</script>

<style></style>