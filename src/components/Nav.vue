<template>
    <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
      <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="#">Company name</a>

      <ul class="navbar-nav px-3">
        <li class="nav-item text-nowrap">
          <router-link to="/profile" class="nav-link" href="#">{{user.first_name}} {{user.last_name}}</router-link>
          <a class="nav-link" href="#" @click="logout">Sign out</a>
        </li>
      </ul>
    </nav>
</template>

<script>
import axios from 'axios'

export default {
  name: "Nav",
  methods: {
    async logout() {
      await axios.post('logout');

      await this.$router.push('/login');
    }
  },
  computed: {
    user() {
      return this.$store.state.user;
    }
  }
}
</script>

<style>
  .nav-item {
    display: flex;
    flex-direction: row;
    padding: 10px;
  }
  .nav-item a {
    margin: 0px 5px;
  }
</style>