<template>
  <div class="login-wrapper">
    <h1><span class="title-color">Lead</span>Hit</h1>
    <form class="login-form" @submit.prevent="login">
      <h5>Авторизация</h5>
      <div class="form-group">
        <input
            class="id-input-input_id"
            placeholder="Введите ID сайта"
            type="text"
            v-model="id"
            maxlength="24"
            :style="id.length > 0 ? 'width: 250px;' : ''"
        />
        <span v-if="error" class="id-error">{{ error }}</span>
      </div>
      <button type="button" @click="login" class="btn">Войти</button>
    </form>

<!--    <span v-if="error" class="id-error">{{ error }}</span>-->
  </div>

</template>

<script>
import {mapActions} from "vuex";
import {REQUEST_AUTH} from "@/store/action-types";

export default {
  name: "HomeView",
  data() {
    return {
      id: "",
      error: "",
    };
  },
  watch: {
    id: function () {
      if (this.id.length) {
        this.error = "";
      } else {
        this.error = "Id сайта должен содержать 24 символа!";
      }
    },
  },
  methods: {
    ...mapActions({
      auth: REQUEST_AUTH,
    }),
    login() {
      if (this.id.length === 24) {
        this.auth(this.id).then((res) => {
          if (!res.error) {
            const {message} = res;
            if (message && message === "ok") {
              this.$router.push({path: "/analytics"});
            }
          } else {
            this.error = res.error;
          }
        });
      } else {
        this.error = "Id сайта должен содержать 24 символа!";
      }
    },
  },
  beforeDestroy() {
    this.id = "";
    this.error = "";
  },
};
</script>

<style scoped lang="scss">
.title-color {
  color: #ff5715;
}

.login-title {
  margin: 0;
}

.login-wrapper {
  background: rgba(1, 1, 1, .4);
  height: 100vh;
  padding-top: 10vh;
}

.login-form {
  box-sizing: border-box;
  margin: 0 auto;
  margin-top: 60px;
  padding: 50px;
  border: 1px solid #ccc;
  border-radius: 20px;
  box-shadow: 0 0 24px #bfbdbd;
  width: 20%;
  background-color: #ccc;
}

.btn {
  background-color: #ff5715;
  //color: #ffffff;
  box-shadow: 0 0 10px #ff5715;
}

</style>
