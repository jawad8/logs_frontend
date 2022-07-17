<template>
    <h1>Welcome to logs Display console</h1>
    <div>
        <button class="createUser">Create User</button>
        <br/>
        <br/>
        <button class="viewLogs">View Logs</button>
        <br/>
        <br/>
        <v-table>
            <tr>
                <th>Log Type</th>
                <th>Log Message</th>
                <th>Time</th>
            </tr>
            <tr>
                <td>Warnng</td>
                <td>this is a warning</td>
                <td>11:30pm</td>
            </tr>
            <tr>
                <td>Info</td>
                <td>this is info</td>
                <td>12:00pm</td>
            </tr>
        </v-table>
    </div>
</template>
<script>
import {createApp} from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
import App from '../App.vue'
const app = createApp(App)
app.use(VueAxios,axios)
export default {
    name: 'HomePage',
    mounted(){
        app.axios.get('http://127.0.0.1:8000/logs/fetchLogs/').then((res)=>{
            console.warn(res)
        })
    }
}
</script>