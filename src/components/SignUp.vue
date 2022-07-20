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

@import "https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css";
@import"https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js";
@import "https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js";
</style>

<template>
  <div>
    <h1>Logs Display Mechanism </h1>
    <form class="loginForm">
      <div class="imgcontainer">
        <img src="../assets/login.svg" alt="Avatar" class="avatar">
      </div>
      <div class="container loginCreds">
        <label for="uname"><b>Username</b></label>
        <input type="text" placeholder="Enter Username" name="uname" class="username" required>
        <br />
        <label for="psw"><b>Password</b></label>
        <input type="password" placeholder="Enter Password" name="psw" class="password" required>
        <br />
        <button type="button" @click="greet">Sign in</button>
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
    greet() {
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