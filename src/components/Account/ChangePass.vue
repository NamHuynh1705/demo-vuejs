<template>
  <b-form @submit="onSubmitChangePass" @reset="onReset">
    <b-form-group
      id="input-group-1"
      label="Current Password:"
      label-for="input-1"
    >
      <b-form-input
        id="input-1"
        v-model.trim="changePass.pass"
        type="password"
        placeholder="Enter Current Password"
        required
      ></b-form-input>
    </b-form-group>
    <b-form-group id="input-group-2" label="New Password:" label-for="input-2">
      <b-form-input
        id="input-2"
        v-model.trim="changePass.newpass"
        type="password"
        placeholder="Enter New Password"
        required
      ></b-form-input>
    </b-form-group>
    <b-form-group
      id="input-group-2"
      label="Confirm New Password:"
      label-for="input-2"
    >
      <b-form-input
        id="input-2"
        v-model.trim="changePass.confirm"
        type="password"
        placeholder="Confirm New Password"
        required
      ></b-form-input>
    </b-form-group>
    <p class="notification">{{ notification }}</p>
    <div class="group-button-login">
      <b-button type="submit" variant="success">Save</b-button>
      &emsp;
      <b-button type="reset">Cancel</b-button>
    </div>
  </b-form>
</template>

<script>
export default {
  name: "ChangePass",
  data() {
    return {
      changePass: {
        pass: "",
        newpass: "",
        confirm: "",
      },
      notification: "",
    };
  },
  props: {
    account: Object,
  },
  methods: {
    onSubmitChangePass(e) {
      e.preventDefault();
      let textPass = this.changePass;
      let textAccount = this.account;
      if (
        textPass.pass === textAccount.password &&
        textPass.newpass === textPass.confirm &&
        textPass.newpass.length >= 8 &&
        textPass.confirm.length >= 8
      ) {
        this.$emit("changePass", textPass.newpass);
        this.$emit("setModelChangePass", false);
        this.$emit("showAlert", true);
      } else if (textPass.pass !== textAccount.password) {
        this.notification = "Entered Wrong Password!";
      } else if (textPass.newpass.length < 8) {
        this.notification = "New Password Must Be At Least 8 Characters!";
      } else if (textPass.newpass !== textPass.confirm) {
        this.notification =
          "The New Password And Confirmation Fields Must Be The Same!";
      }
    },
    onReset() {
      this.notification = "";
    },
  },
};
</script>

<style>
</style>