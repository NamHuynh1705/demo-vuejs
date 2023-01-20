<template>
  <div class="menu">
    <ul>
      <div class="nav-img">
        <img class="logo-menu" alt="logo" src="../../assets/logo.png" />
        <p class="label-menu">Menu VueJS</p>
      </div>
      <li
        :class="{ activeMenu: activeMenu == 'home' }"
        @click="setActive('home')"
      >
        <router-link to="/"
          ><b-icon class="icon-menu" icon="house-door-fill"></b-icon
          >Home</router-link
        >
      </li>
      <li
        :class="{ activeMenu: activeMenu == 'action' }"
        @click="setActive('action')"
      >
        <router-link to="/action"
          ><b-icon class="icon-menu" icon="star-half"></b-icon
          >Action</router-link
        >
      </li>
      <li
        :class="{ activeMenu: activeMenu == 'table' }"
        @click="setActive('table')"
      >
        <router-link to="/table"
          ><b-icon class="icon-menu" icon="table"></b-icon>Table</router-link
        >
      </li>
      <li
        :class="{ activeMenu: activeMenu == 'table-api' }"
        @click="setActive('table-api')"
      >
        <router-link to="/table-api"
          ><b-icon class="icon-menu" icon="arrow-down-circle"></b-icon>Table
          API</router-link
        >
      </li>
      <li
        :class="{ activeMenu: activeMenu == 'vuetify' }"
        @click="setActive('vuetify')"
      >
        <router-link to="/vuetify"
          ><b-icon class="icon-menu" icon="emoji-sunglasses"></b-icon
          >Vuetify</router-link
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Menu",
  data() {
    return {
      activeMenu: "",
    };
  },
  props: {
    labelNavbar: String,
  },
  methods: {
    setActive(menu) {
      this.activeMenu = menu;
      let data = {
        labelNavbar: menu,
      };
      this.$emit("changLableNavbar", data);
    },
  },
  beforeMount() {
    let url = window.location.href.split("/");
    let menu = url[url.length - 1];
    if (menu == "") menu = "home";
    this.activeMenu = menu;
  },
};
</script>

<style scoped>
ul {
  box-sizing: border-box;
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #f1f1f1;
  position: fixed;
  height: 100%;
  overflow: auto;
}
.menu {
  height: 100vh;
}
.logo-menu {
  width: 42%;
}
.nav-img {
  width: 100%;
  text-align: center;
  margin-top: 10px;
  margin-bottom: 40px;
}
.label-menu {
  margin-top: 0px;
  font-style: italic;
  color: #22c786;
  font-weight: bold;
  text-shadow: 0px 1px #22c786;
  font-size: 20px;
}
.icon-menu {
  margin-right: 10px;
}
ul li {
  width: 100%;
  height: 40px;
  margin-top: 15px;
}
ul li a {
  text-decoration: none;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  transition: all 0.3s ease;
  color: #000;
  font-weight: bold;
  font-size: 18px;
  padding: 15px 50px 15px 49px;
}
.activeMenu a {
  background-color: #22c786;
  color: #ffff;
}
ul li a:hover {
  background-color: #22c786;
  color: #ffff;
}
</style>