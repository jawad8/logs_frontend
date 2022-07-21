<style>
.avatar {
  width: 200px;
  margin-bottom: 10px;
}

.loginForm {
  border: 3px solid #f1f1f1
}

.loginCreds input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}

.loginCreds button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
.signup_header{
      margin-top: -60px;
    background-color: black;
}
@import "https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css";
@import"https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js";
@import "https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js";
</style>

<template>
  <div>
    <div class="signup_header">
    <h1>Logs Display Mechanism </h1></div>
    <form class="loginForm">
      <div class="imgcontainer" style="padding: 15px;">
        <img src="../assets/login.svg" alt="Avatar" class="avatar">
      </div>
      <div class="container loginCreds mb-3" style="background-color: beige">
        <label for="username"><b>Username</b></label>
        <input type="text" placeholder="Enter Username" name="username" class="username" required>
        <br />
        <label for="password"><b>Password</b></label>
        <input type="password" placeholder="Enter Password" name="password" class="password" required>
        <br />
        <button type="button" @click="login">Sign in</button>
      </div>
    </form>
  </div>
</template>
<script>
import axios from 'axios'
import $ from "jquery";


export default {
  data() {
    return {
      name: 'Vue.js'
    }
  },
  methods: {
    login() {
      var username = $(".username").val()
      var password = $(".password").val()
      var authData = {
        "Username": username,
        "password": password,
      }
      axios.post("http://127.0.0.1:8000/users/authUser/", authData).then((response) => {
        if (response.data) {
          this.$router.push({ name: 'HomePage' })
        }
        else{
          alert("Please enter correct username and password")
        }
      })
    }
  }
}
</script>