<template>
  <div id="Navbar">
    <div class="label-navbar"></div>
    <div class="group-button">
      <p class="hello-name" v-if="model === 'Logout'">
        Hello, {{ account.name }}
      </p>
      <b-dropdown variant="info">
        <template #button-content>
          <b-icon icon="gear-fill" aria-hidden="true"></b-icon> Settings
        </template>
        <b-dropdown-item-button>
          <b-icon icon="people-fill" aria-hidden="true"></b-icon>
          Profile
        </b-dropdown-item-button>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item-button
          v-b-modal.modal-2
          @click="showModalChangePass(true)"
          :disabled="model === 'Login'"
          >Change Password</b-dropdown-item-button
        >
        <b-dropdown-item-button>Language</b-dropdown-item-button>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item-button
          v-if="model === 'Login'"
          v-b-modal.modal-1
          variant="danger"
        >
          <b-icon icon="arrow-bar-right" aria-hidden="true"></b-icon>
          Login
        </b-dropdown-item-button>
        <b-dropdown-item-button
          v-if="model === 'Logout'"
          @click="handleLogout"
          variant="danger"
        >
          <b-icon icon="arrow-bar-left" aria-hidden="true"></b-icon>
          Logout
        </b-dropdown-item-button>
      </b-dropdown>
      <b-modal
        v-if="model === 'Login'"
        id="modal-1"
        title="Login"
        :hide-footer="true"
      >
        <div>
          <Login :account="account" @changeModelLogin="changeModelLogin" />
        </div>
      </b-modal>
      <b-modal
        v-if="modalChangePass"
        id="modal-2"
        title="ChangePass"
        :hide-footer="true"
      >
        <div>
          <ChangePass
            :account="account"
            @showAlert="showAlert"
            @changePass="changePass"
            @setModelChangePass="setModelChangePass"
          />
        </div>
      </b-modal>
    </div>
    <b-toast
      class="alert-changepass"
      v-if="setAlert === true"
      id="example-toast"
      title="Notification"
      static
      visible
      auto-hide-delay="3000"
      variant="success"
    >
      ✔ Change password successfully!
    </b-toast>
  </div>
</template>

<script>
import Vue from "vue";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import Login from "../Account/Login.vue";
import ChangePass from "../Account/ChangePass.vue";
Vue.use(BootstrapVue);
Vue.use(IconsPlugin);
export default {
  name: "Navbar",
  components: {
    Login,
    ChangePass,
  },
  data() {
    return {
      account: {
        name: "User Name",
        username: "admin",
        password: "password",
      },
      model: "Login",
      modalChangePass: true,
      setAlert: false,
    };
  },
  props: {
    labelNavbar: String,
  },
  methods: {
    changeModelLogin(e) {
      this.model = e;
    },
    handleLogout() {
      if (this.model === "Logout") {
        this.model = "Login";
      }
    },
    changePass(e) {
      this.account.password = e;
    },
    setModelChangePass(e) {
      this.modalChangePass = e;
    },
    showModalChangePass(e) {
      this.modalChangePass = e;
    },
    showAlert(e) {
      this.setAlert = e;
      setTimeout(() => {
        this.setAlert = false;
      }, 3000);
    },
  },
  beforeMount() {
    let url = window.location.href.split("/");
    let label = url[url.length - 1];
    if (label == "") label = "Home";
    label = label.toUpperCase();
    let data = {
      labelNavbar: label,
    };
    this.$emit("changLableNavbar", data);
  },
};
</script>

<style scoped>
#Navbar {
  width: 100%;
  height: 60px;
  border-bottom: 1px solid #ccc;
  box-shadow: 0px 2px 7px #f1f1f1;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
p {
  margin: unset;
  margin-left: 30px;
  color: #000;
  font-style: inherit;
  font-size: 22px;
}
.group-button {
  display: flex;
}
.group-button {
  margin-top: 5px;
  margin-right: 30px;
}
.hello-name {
  font-size: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 15px;
}
.alert-changepass {
  position: absolute;
  top: 67px;
  right: 27px;
}
</style>