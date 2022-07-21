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

.logTable label{
    font-weight: 500;
}
.heading{
    margin-top: -60px;
    background-color: black;
}
.filter_title{
    font-weight: 700;
    text-align: left;
}
.bodyTab{
    background-color: beige;
}
</style>
<template>
<div class="heading">
    <h1 class="display-2">Welcome to logs Display console</h1></div>
    <div class="buttonDiv">
        <button type="button" class="btn btn-primary createUser" @click="userToggle">Create User</button>
        <button type="button" class="btn btn-primary viewLogs" @click="viewLogs">View Logs</button>
        <hr />
    </div>
    <div class="bodyTab">
        <div class="logTable hide container row">
            <div class="col-3">
                <p class="filter_title">Log Type Filter</p>

                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="20" @change="checkFilter" id="info">
                    <label class="form-check-label" for="flexCheckDefault">
                        Info
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="40" @change="checkFilter" id="error">
                    <label class="form-check-label" for="flexCheckDefault">
                        Error
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="10" @change="checkFilter" id="debug">
                    <label class="form-check-label" for="flexCheckDefault">
                        Debug
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="50" @change="checkFilter" id="critical">
                    <label class="form-check-label" for="flexCheckDefault">
                        Critical
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="30" @change="checkFilter" id="warning">
                    <label class="form-check-label" for="flexCheckDefault">
                        Warning
                    </label>
                </div>
                <div style="margin-top: 10px;">
                    <p class="filter_title">Logs time filter</p>
                                    <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="today" @change="checkFilter" id="today">
                    <label class="form-check-label" for="flexCheckDefault">
                        Today
                    </label>
                </div>
                <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="yesterday" @change="checkFilter" id="yesterday">
                    <label class="form-check-label" for="flexCheckDefault">
                        Yesterday
                    </label>
                </div>
                </div>
                <button type="button" class="btn btn-primary createUser" @click="applyFilter">Apply filter</button>
            </div>
            <div class="col-9">
                <h2>Logs Table</h2>
            <table class="table table-bordered" style="margin-bottom:100px" id="datatable">
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
        </div>
        <div class="container createUserTab hide">
            <div class="form-group">
                <label for="Username">User Name</label>
                <input type="text" class="form-control" id="Username" placeholder="User name">
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" class="form-control" id="password" placeholder="Password">
            </div>
            <button type="button" class="btn btn-primary" @click="createUser">Create User</button>
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
    data: function () {
        return {
            products: [],
        };
    },
    methods: {
        viewLogs() {
            $(".logTable").removeClass("hide")
            $(".createUserTab").addClass("hide")
            axios.get("http://127.0.0.1:8000/logs/fetchLogs/").then((response) => {
                this.products = response.data;
                $("#datatable").DataTable();
            });
        },
        userToggle() {
            $(".createUserTab").removeClass("hide")
            $(".logTable").addClass("hide")
        },
        checkFilter(x) {
            if (x.target.classList.contains("check")) {
                x.target.classList.remove("check")
            }
            else {
                x.target.classList.add("check")
            }
        },
        applyFilter() {
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
        createUser() {
            var create_userData = {
                "Username": $("#Username").val(),
                "password": $("#password").val(),
                "user_type": "user"
            }
            axios.post("http://127.0.0.1:8000/users/createuser/", create_userData).then((response) => {
                if (response.data) {
                    alert("User created!")
                }
                else {
                    alert("Something went wrong please try again")
                }
            });
        }
    }
}
</script>