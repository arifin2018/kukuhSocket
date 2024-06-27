<template>
    <div>
        <h1>Please login before login our chat</h1>
        <input type="text" name="login-name" :value="name" @input="e=>onChange(e.target.value)>   
        <button type="button>Submit</button>
    </div>
</template>

<script>
export default {
    props: {
        name: String,
        onChange: Function
    }
}
</script>