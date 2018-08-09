<template>
    <aside>
        <div class="server-controls">
            <TextButton v-on:add="$emit('add-server')" icon="+" text="Add Server" event="add"/>
            <TextButton v-on:destroy="$emit('destroy-server')" icon="-" text="Destroy" event="destroy"/>
        </div>
        <h3>Available Apps</h3>
        <AppUnit v-on:add-app="$emit('add-app', app.event)" v-on:remove-app="$emit('remove-app', app.event)" v-for="app in availableApps" :key="app.appName" 
            :appName="app.appName" :color="app.color"/>
    </aside>
</template>

<script>
import TextButton from '@/components/TextButton.vue';
import AppUnit from '@/components/AppUnit.vue';

export default {
    name: 'Sidebar',
    components: {
        TextButton,
        AppUnit
    },
    props: {
        availableApps: { // Ideally would grab this from config file.
            default: function () { return [
                {appName: "Hadoop", color: "hotpink", event: "hd"}, 
                {appName: "Rails", color: "blueviolet", event: "rl"},
                {appName: "Chronos", color: "cyan", event: "ch"},
                {appName: "Storm", color: "turquoise", event: "st"},
                {appName: "Spark", color: "chartreuse", event: "sp"}
            ]},
            type: Array
        }
    }
}
</script>

<style scoped>
aside {
    background-color: grey;
    width: 300px;
    align-items: center;
}
.server-controls {
    margin: 50px auto 150px;
    width: 130px;
    display: flex;
    justify-content: space-between;
}
h3 {
    text-align: left;
    margin-left: 30px;
}
</style>