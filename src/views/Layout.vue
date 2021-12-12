<template>
<v-app>
  <Nav />
    <div class="container-fluid">
      <div class="row">
        <Menu/>
        <main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
          <div class="table-responsive">
            <router-view />
          </div>
        </main>
      </div>
    </div>
    </v-app>
</template>

<script lang="ts">
import axios from "axios";
import Nav from '@/components/Nav.vue';
import Menu from '@/components/Menu.vue';
import {User} from '@/models/user';

export default {
    name: "Layout",
    components: { Nav, Menu },
    async mounted() {
      try {
        const {data} = await axios.get('user');

        await this.$store.dispatch('setUser', data);
      } catch (e) {
        await this.$router.push('/login');
      }
    }
}
</script>

<style>
.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: 0 auto;
}
.form-signin .checkbox {
  font-weight: 400;
}
.form-signin .form-control {
  position: relative;
  box-sizing: border-box;
  height: auto;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>