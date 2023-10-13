<template>
  <div id="app">
    <div v-if="!isSuccess">
      <AppForm
        :defaultValues="defaultValues"
        :roles="roles"
        :errors="errors"
        @sendForm="sendForm($event)"
      />
      <p class="error-text">{{ errorText }}</p>
    </div>

    <div v-else class="success-text">
      <h1>Регистрация успешно завершена!</h1>
    </div>
  </div>
</template>

<script>
import AppForm from "./components/AppForm.vue";

export default {
  components: { AppForm },
  data: () => ({
    isSuccess: false,
    defaultValues: {
      username: "test name",
      role: 3,
      email: "test@ya.ru",
      password: "123",
      password_repeat: "123",
    },
    roles: [
      { value: 1, name: "Test 1" },
      { value: 2, name: "Test 2" },
      { value: 3, name: "Test 3" },
    ],
    errors: {},
    errorText: "",
  }),
  methods: {
    sendForm(data) {
      const xhr = new XMLHttpRequest();
      xhr.open("POST", "https://lmstestapi.reezonly.com/v1/user/signup");
      xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
      xhr.send(JSON.stringify(data));
      xhr.onload = () => {
        const data = JSON.parse(xhr.response);
        if (data.success) {
          this.isSuccess = true;
          return;
        }

        this.errors = data.errors;
      };
      xhr.onerror = () => {
        this.errorText = "Ошибка " + xhr.statusText;
      };
    },
  },
};
</script>

<style>
@import "./assets/fonts/link.css";

* {
  margin: 0;
  padding: 0;
}
#app * {
  font-family: "Montserrat", sans-serif;
}
.success-text {
  text-align: center;
  margin-top: 30px;
  color: #001803;
}
.error-text {
  color: red;
  text-align: center;
  margin-bottom: 20px;
}
</style>
