<template>
    <div class="app-unit" v-bind:style="{ borderColor: color }">
        <label>{{ appName }}</label>

        <div>
            <button v-on:click="$emit('remove-app')">-</button>
            <button v-on:click="$emit('add-app')" v-bind:style="{ backgroundColor: color }">+</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AppUnit',
    props: {
        appName: String,
        color: String,
        event: String
    }
}
</script>

<style scoped>
.app-unit {
    border-style: solid;
    border-width: 0 0 0 10px;
    height: 50px;
    background-color: rgba(0,0,0,0.6);
    display: flex;
    align-items: center;
    justify-content: space-between;
}
label {
    color: white;
    margin-left: 20px;
}
button {
    border-radius: 50%;
    margin: 0 0 0 5px;
}
</style>