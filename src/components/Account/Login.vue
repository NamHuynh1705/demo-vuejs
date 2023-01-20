<template>
  <div>
    <b-form @submit="onSubmitLogin" @reset="onReset">
      <b-form-group id="input-group-1" label="User Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model.trim="login.username"
          type="text"
          placeholder="Enter UserName"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label="Password:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model.trim="login.password"
          type="password"
          placeholder="Enter Password"
          required
        ></b-form-input>
      </b-form-group>
      <p class="notification">{{ notification }}</p>
      <div class="group-button-login">
        <b-button type="submit" variant="success">Login</b-button>
        &emsp;
        <b-button type="reset">Cancel</b-button>
      </div>
    </b-form>
  </div>
</template>

<script>
import Vue from "vue";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
Vue.use(BootstrapVue);
Vue.use(IconsPlugin);
export default {
  name: "Login",
  data() {
    return {
      login: {
        username: "",
        password: "",
      },
      notification: "",
    };
  },
  props: {
    account: Object,
  },
  methods: {
    onSubmitLogin(e) {
      e.preventDefault();
      let textLogin = this.login;
      let textAccount = this.account;
      if (
        textLogin.username == textAccount.username &&
        textLogin.password == textAccount.password
      ) {
        this.notification = "Logged in successfully";
        this.$emit("changeModelLogin", "Logout");
      } else if (textLogin.username !== textAccount.username) {
        this.notification = "Username is not correct, please re-enter!";
      } else if (textLogin.password !== textAccount.password) {
        this.notification = "Password is not correct, please re-enter!";
      }
    },
    onReset() {
      this.notification = "";
    },
  },
};
</script>

<style>
.group-button-login {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 15px;
  margin-bottom: 5px;
}
.notification {
  color: #ff0000bd;
  font-style: italic;
  margin: auto;
  display: flex;
  justify-content: center;
}
</style>