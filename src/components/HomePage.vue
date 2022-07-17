<template>
<h1>Welcome to logs Display console</h1>
<div>
    <button class="createUser">Create User</button>
    <br />
    <br />
    <v-modal class="createUserModal">
        <p class="my-4">Hello from modal!</p>
    </v-modal>
    <button class="viewLogs">View Logs</button>

</div>
</template>
<script>
export default {
    name : 'HomePage'
}
</script>