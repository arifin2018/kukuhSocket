<template>
    <div class="p-3 text-center">
        <h1>Please login before login our chat</h1>
            <input class="border border-black rounded-sm mr-2" type="text" name="login-name" :value="name" @input="onChangeText">   
            <button type="button" class="bg-blue-300 rounded-sm p-1 text-sm" @click="tokai">Submit</button>
    </div>
</template>

<script>
export default {
    props: {
        name: String,
        onChange: Function,
        isRegistered: Boolean
    },
    methods: {
        onChangeText(e){
            this.$props.onChange(e.target.value)
        },
        tokai(e){
            this.$emit("dataIsRegistered", !this.$props.isRegistered);
            console.log(e);
        }   
    },
}
</script>