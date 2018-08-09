<template>
    <div class="server-canvas">
        <h1>Server Canvas</h1>
        <div class="server-grid" v-bind:style="{ height: setHeight + 'px' }">
            <ServerUnit v-for="n in serverCount" :key="n" :serverData="servers[n-1]"/>
        </div>
    </div>
</template>

<script>
import ServerUnit from '@/components/ServerUnit.vue';

export default {
    name: 'ServerCanvas',
    components: {
        ServerUnit
    },
    props: {
        serverCount: Number,
        servers: Array
    },
    computed: {
        setHeight: function () {
            return (150 + 15) * Math.ceil(this.serverCount / 4);
        }
    }
}
</script>

<style>
.server-canvas {
    width: 940px; /*can use computed if config set to serverunit width + 15 * 4*/
    margin: auto;
    background-color: black;
}
h1 {
    text-align: left;
    color: white;
}
.server-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
</style>