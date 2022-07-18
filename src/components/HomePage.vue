<style>
.viewLogs {
    margin-left: 30%;

}

.buttonDiv {
    margin-top: 2%;
}

.hide {
    display: none;
}

.createUserTab {
    width: 30% !important;
}

.logTable th {
    text-align: center;
}

.form-check {
    width: 4px;
}
</style>
<template>
    <h1 class="display-2">Welcome to logs Display console</h1>
    <div class="buttonDiv">
        <button type="button" class="btn btn-primary createUser" @click="showUser">Create User</button>
        <button type="button" class="btn btn-primary viewLogs" @click="show">View Logs</button>
        <hr />
    </div>
    <div>
        <div class="logTable hide container">
            <div>
                <label style="margin-left: -1075px;">Log Type Filter</label>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="20" @change="checkFiltr" id="info">
                    <label class="form-check-label" for="flexCheckDefault">
                        Info
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="40" @change="checkFiltr" id="error">
                    <label class="form-check-label" for="flexCheckDefault">
                        Error
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="10" @change="checkFiltr" id="debug">
                    <label class="form-check-label" for="flexCheckDefault">
                        Debug
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="50" @change="checkFiltr" id="critical">
                    <label class="form-check-label" for="flexCheckDefault">
                        Critical
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="30" @change="checkFiltr" id="warning">
                    <label class="form-check-label" for="flexCheckDefault">
                        Warning
                    </label>
                </div>
                <button type="button" class="btn btn-primary createUser" @click="filter">Apply filter</button>
            </div>
            <h2>Logs Table</h2>
            <table class="table table-bordered" id="datatable">
                <tbody>
                    <tr>
                        <th>ID</th>
                        <th>Log Type</th>
                        <th>Log Time</th>
                        <th>Log Error Message</th>
                    </tr>
                    <tr v-for="item in products" :key="item.id">
                        <td>{{ item.id }}</td>
                        <td>{{ item.log_type }}</td>
                        <td>{{ item.log_time }}</td>
                        <td>{{ item.log_error_Message }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="container createUserTab hide">
            <div class="form-group">
                <label for="Username">User Name</label>
                <input type="text" class="form-control" id="Username" placeholder="User name">
            </div>
            <div class="form-group">
                <label for="passwd">Password</label>
                <input type="password" class="form-control" id="passwd" placeholder="Password">
            </div>
            <button type="button" class="btn btn-primary">Create User</button>
        </div>
    </div>
</template>
<script>
import { createApp } from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';
import App from '../App.vue'
import "jquery/dist/jquery.min.js";
import "bootstrap/dist/css/bootstrap.min.css";
import "datatables.net-dt/js/dataTables.dataTables";
import "datatables.net-dt/css/jquery.dataTables.min.css";
import $ from "jquery";

const app = createApp(App)
app.use(VueAxios, axios, $)
export default {
    name: 'HomePage',
    mounted() {

    },
    data: function () {
        return {
            products: [],
        };
    },
    methods: {
        show() {
            $(".logTable").removeClass("hide")
            $(".createUserTab").addClass("hide")
            axios.get("http://127.0.0.1:8000/logs/fetchLogs/").then((response) => {
                this.products = response.data;
                $("#datatable").DataTable();
            });
        },
        showUser() {
            $(".createUserTab").removeClass("hide")
            $(".logTable").addClass("hide")
        },
        filter() {
            var filterReq = {}
            $('.form-check-input').map(function (val, x) {
                if (x.classList.contains("check")) {
                    filterReq[x.id] = x.value

                }
            });
            axios.post("http://127.0.0.1:8000/logs/filterLogs/", filterReq).then((response) => {
                this.products = response.data;
                $("#datatable").DataTable();
            });
        },
        checkFiltr(x) {
            if (x.target.classList.contains("check")) {
                x.target.classList.remove("check")

            }
            else {
                x.target.classList.add("check")
            }
        }
    }
}
</script>