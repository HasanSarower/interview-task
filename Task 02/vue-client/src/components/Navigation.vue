<template>
  <nav class="navbar navbar-expand navbar-dark bg-dark">
    <div class="container">
      <div class="navbar-header">
        <router-link class="navbar-brand" to="/">Admin Dashboard</router-link>
      </div>
      <ul class="nav navbar-nav">
        <router-link v-if="!isLoggedIn" class="nav-item nav-link" :to="{ name: 'Login' }">Login</router-link>
        <router-link
          v-if="!isLoggedIn"
          class="nav-item nav-link"
          :to="{ name: 'Register' }"
        >Register</router-link>
        <router-link
          v-if="isLoggedIn"
          class="nav-item nav-link"
          :to="{ name: 'Dashboard' }"
        >User List</router-link>
        <router-link
          v-if="isLoggedIn"
          class="nav-item nav-link"
          :to="{ name: 'Role_list' }"
        >Role List</router-link>
        <!-- <router-link class="nav-item nav-link" v-if="isLoggedIn" @click.prevent="logout"> Logout </router-link> -->
        <a class="nav-item nav-link" v-if="isLoggedIn" @click.prevent="logout" >Logout</a>
      </ul>
    </div>
  </nav>
</template>

<script>
import User from "../apis/User";
import { mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters(["isLoggedIn"])
  },

  methods: {
    logout() {
      User.logout().then(() => {
        localStorage.removeItem("token");
        this.$store.commit("LOGIN", false);
        this.$router.push({ name: "Home" });
      });
    }
  }
};
</script>

<style>
.router-link-exact-active {
  color: #ffffff !important;
  transition: all 0.25s;
}
</style>
