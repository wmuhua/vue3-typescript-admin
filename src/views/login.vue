<script setup lang="ts">
import { ref, computed } from "vue";
import { useRouter } from "vue-router";
import { initRouter } from "/@/router";
import { storageSession } from "/@/utils/storage";
import { addClass, removeClass } from "/@/utils/operate";
import bg from "/@/assets/login/bg.png";

const router = useRouter();

let user = ref("admin");
let pwd = ref("123456");

const onLogin = (): void => {
  storageSession.setItem("info", {
    username: "admin",
    accessToken: "eyJhbGciOiJIUzUxMiJ9.test",
  });
  initRouter("admin").then(() => {});
  router.push("/");
};

function onUserFocus() {
  addClass(document.querySelector(".user"), "focus");
}

function onUserBlur() {
  if (user.value.length === 0)
    removeClass(document.querySelector(".user"), "focus");
}

function onPwdFocus() {
  addClass(document.querySelector(".pwd"), "focus");
}

function onPwdBlur() {
  if (pwd.value.length === 0)
    removeClass(document.querySelector(".pwd"), "focus");
}
</script>

<template>
  <img :src="bg" class="wave" />
  <div class="container">
    <div class="login-box">
      <div class="login-form">
        <!-- <avatar class="avatar" /> -->
        <h2>生活服务管理</h2>
        <div class="input-group user focus">
          <div class="icon">
            <i class="fa fa-user"></i>
          </div>
          <div>
            <h5>用户名</h5>
            <input
              type="text"
              class="input"
              v-model="user"
              @focus="onUserFocus"
              @blur="onUserBlur"
            />
          </div>
        </div>
        <div class="input-group pwd focus">
          <div class="icon">
            <i class="fa fa-lock"></i>
          </div>
          <div>
            <h5>密码</h5>
            <input
              type="password"
              class="input"
              v-model="pwd"
              @focus="onPwdFocus"
              @blur="onPwdBlur"
            />
          </div>
        </div>
        <button class="btn" @click="onLogin">登录</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("/@/style/login.css");
</style>
