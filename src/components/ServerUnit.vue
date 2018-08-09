<template>
    <div class="server-unit" v-bind:style="{ backgroundColor: randomColor }">
        <label v-for="(value, key) in serverData" :key=key>{{ value }}</label>
    </div>
</template>

<script>
export default {
    name: 'ServerUnit',
    props: { 
        availableApps: { // Ideally would grab this from config file.
            default: function () { return [ // Must use factory pattern or else every instance will share the same thing when I not passing target property to this component.
                {appName: "Hadoop", abbr: "Hd", color: "hotpink"}, 
                {appName: "Rails", abbr: "Rl", color: "blueviolet"},
                {appName: "Chronos", abbr: "Ch", color: "cyan"},
                {appName: "Storm", abbr: "St", color: "turquoise"},
                {appName: "Spark", abbr: "Sp", color: "chartreuse"}
            ]},
            type: Array
        },
        serverData: Array
    },
    computed: {
        randomColor: function () {
            return 'rgba(' + Math.ceil(Math.random() * 225) + ',' + Math.ceil(Math.random() * 225) + ',' + Math.ceil(Math.random() * 225) + ',0.5)'
        }
    }
}
</script>

<style>
.server-unit {
    width: 220px; /*~0.7 ratio*/
    height: 150px;
    background-color: grey;
    border-radius: 5px;
}
label {
    color: white;
}
</style>