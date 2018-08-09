<template>
    <div class="root">
        <Sidebar v-on:add-server="addServer" v-on:destroy-server="destroyServer" 
            v-on:add-app="addApp" v-on:remove-app="removeApp"/>
        <ServerCanvas :serverCount="serverCount" :servers="servers"/>
    </div>
</template>

<script>
import Sidebar from '@/components/Sidebar.vue';
import ServerCanvas from '@/components/ServerCanvas.vue';

export default {
    name: 'DataCenterManagement',
    components: {
        Sidebar,
        ServerCanvas
    },
    props: {
        MAX_APP_PER_SERVER: {
            default: 2,
            type: Number
        }
    },
    data: function () {
        return {
            appCount: 0,
            serverCount: 4,
            apps: { //servers the apps are installed on.
                "hd": [],
                "rl": [],
                "ch": [],
                "st": [],
                "sp": []
            },
            servers: [ //starting out with 4 servers.
                [],
                [], 
                [], 
                []
            ]
        }
    },
    methods: {
        addApp: function (event) {
            if (this.appCount == this.serverCount * 2) { //no space to add apps
                return;
            }

            let i;
            for (i = 0; i < this.serverCount; i++) { //find available server. if performance issue then compute avail servers ahead of time and store.
                if (this.servers[i].length !== 2) { //javascript
                    this.servers[i].push(event); //installed app on server
                    this.apps[event].push(i); //reference integrity
                    break;
                }
            }
            this.appCount++;

            // console.log("ADDED " + event + ". APP COUNT IS " + this.appCount);
        },
        removeApp: function (event) {
            if (this.appCount == 0 || this.apps[event].length == 0) { //no apps to remove
                return;
            }

            let serverId = this.apps[event].pop(), i;
            for (i = 0; i < this.MAX_APP_PER_SERVER; i++) {
                if (this.servers[serverId][i] == event) {
                    this.servers[serverId].splice(i, 1);
                    break;
                }
            }
            this.appCount--;
            
            // console.log("REMOVED " + event + ". APP COUNT IS " + this.appCount);
        },
        addServer: function () {
            this.servers.push([]);
            this.serverCount++; // no server limit
            
            // console.log("ADDED SERVER");
        },
        destroyServer: function () {
            if (this.serverCount == 0) { //nothing to destroy
                return;
            }

            let i = 0, app, lastServer = this.serverCount-1, orphanApps = this.servers[lastServer].length; //number of apps that need to be reallocated on deletion.

            if (orphanApps == 0) { //last server has no apps installed
                this.servers.pop();
                this.serverCount--;
                return;
            }

            //move apps if possible. (servers index happens to also be number of servers when it is gone)
            while(this.appCount - orphanApps !== (lastServer * this.MAX_APP_PER_SERVER)) {
                this.addApp(this.servers[lastServer][i]);
                i++;
            }

            //remove server index from apps data.
            for (i = 0; i < orphanApps; i++) {
                app = this.servers[lastServer][i];
                this.apps[app].splice(this.apps[app].indexOf(lastServer), 1) //not supported in IE7 & 8
            }
            this.appCount -= orphanApps;

            //remove server from servers data.
            this.servers.pop()
            this.serverCount--;
            return;
            
            // console.log("DESTORYED SERVER");
            // console.log(this.apps);
            // console.log(this.servers);
        }
    }
}
</script>

<style>
.root {
    background-color: black;
    display: flex;
}
</style>