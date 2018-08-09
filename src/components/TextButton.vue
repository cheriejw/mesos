<template>
    <div class="text-button">
        <button v-on:click="$emit(event)">{{ icon }}</button>
        <label>{{ text }}</label>
    </div>
</template>

<script>
export default {
    name: 'TextButton',
    props: {
        icon: String,
        text: String,
        event: String
    }
}
</script>

<style scoped>
.text-button {
    display: inline-block;
}
button {
    border-radius: 50%;
    border-width: 3px;
    width: 50px;
    height: 50px;
    font-size: 25px;
    color: white;
    background-color: grey;
    border-color: white;
}
label {
    display: block;
    font-size: 12px;
    color: white;
}
</style>