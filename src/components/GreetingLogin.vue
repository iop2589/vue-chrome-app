<template>
    <div>
        <div v-if="!isLogin">
            <form v-on:submit.prevent="onLoginSubmit" id="login-form" class="hidden todos-form">
                <input v-model="userName" required maxlength="15" type="text" placeholder="What is your name?" />
                <button class="font-color todos-input">Log In</button>
            </form>
        </div>
        <div class="greeting" v-else>
            <h1 class="font-color" id="greeting">Hello ! {{ userName }}</h1>
        </div>
    </div>
</template>

<script>

const USERNAME_KEY = "userName";
export default {
    data: function () {
        return {
            userName: "",
            isLogin: false
        }
    },
    mounted: function  () {
        this.getUserName();
    },
    methods: {
        onLoginSubmit: function () {
            localStorage.setItem(USERNAME_KEY, this.userName);
            this.isLogin = true;
        },
        getUserName: function () {
            let savedUserName = localStorage.getItem(USERNAME_KEY);
            if (savedUserName === null) {
                this.isLogin = false;
            } else {
                this.isLogin = true;
                this.userName = savedUserName;
            }
        }
    }
}
</script>

<style>

</style>