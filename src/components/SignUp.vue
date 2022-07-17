<template>
  <div>
    <h1>Logs Display Mechanism </h1>
    <form action="action_page.php" method="post" class="loginForm">
      <div class="imgcontainer">
    <img src="../assets/login.svg" alt="Avatar" class="avatar">
  </div>
      <div class="container loginCreds">
        <label for="uname"><b>Username</b></label>
        <input type="text" placeholder="Enter Username" name="uname" required>
        <br/>
        <label for="psw"><b>Password</b></label>
        <input type="password" placeholder="Enter Password" name="psw" required>
        <br/>
        <button type="submit" @v-on:click="SignIn">Sign in</button>
      </div>
    </form>
  </div>
</template>



<script>

export default {
    name: 'SignUp',    
    methods:{
      SignIn(){
        this.$router.push({name:'HomePage'})
      }
    }}
  
</script>
<style>
.avatar{
  width: 200px;
  margin-bottom: 10px;
}
.loginForm{
  border: 3px solid #f1f1f1
}
.loginCreds input{
  width:300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.loginCreds button{
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  background:skyblue;
  color: #fff;
  cursor: pointer;
}
</style>