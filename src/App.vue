<template>
  <div id="app">
    <!--    <Logout v-if="isLogin" />-->
    <Login/>
<!--    <router-view/>-->
  </div>
</template>


<script>

import Login from '@/components/Login'
// import Logout from "@/components/Logout.vue";
export default {
  components: {
    Login,
  },
  computed: {
    isLogin() {
      if (this.$route.path === "/auth" || this.$route.path === "/")
        return false;
      else return true;
    },
  },
};
</script>

<style lang="scss">
@import "assets/index.css";
@import "~materialize-css/dist/css/materialize.min.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
