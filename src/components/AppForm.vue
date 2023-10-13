<template>
  <form class="form" @submit.prevent="sendForm">
    <div class="form__head">
      <h1 class="form__title">Регистрация</h1>
    </div>
    <div class="form__body">
      <div class="public">
        <label class="public__label">
          <AppSwitcher
            name="public"
            :check="publicSwitcher"
            @update="publicSwitcher = $event"
          />
          <p>Публичный профиль</p>
        </label>
        <p class="public__desc">
          Включает профиль для просмотра другими пользователями по ссылке
        </p>
      </div>

      <div class="data">
        <h2 class="form__subtitle">Данные</h2>
        <div class="data__row">
          <div>
            <input
              type="text"
              class="input"
              placeholder="Имя"
              name="username"
              v-model="username"
            />
            <p v-for="error in errors.username" :key="error" class="error">
              {{ error }}
            </p>
          </div>
          <div>
            <select
              name="role"
              class="input"
              placeholder="Должность"
              v-model="role"
            >
              <option
                v-for="role in roles"
                :key="role.value"
                :value="role.value"
              >
                {{ role.name }}
              </option>
            </select>
            <p v-for="error in errors.role" :key="error" class="error">
              {{ error }}
            </p>
          </div>
        </div>
        <div class="data__row">
          <div>
            <input
              type="text"
              class="input"
              placeholder="Email"
              name="email"
              v-model="email"
            />
            <p v-for="error in errors.email" :key="error" class="error">
              {{ error }}
            </p>
          </div>
          <div></div>
        </div>
        <div class="data__row">
          <div>
            <input
              type="password"
              class="input"
              placeholder="Пароль"
              name="password"
              v-model="password"
            />
            <p v-for="error in errors.password" :key="error" class="error">
              {{ error }}
            </p>
          </div>
          <div>
            <input
              type="password"
              class="input"
              placeholder="Повторите пароль"
              name="password_repeat"
              v-model="password_repeat"
            />
            <p
              v-for="error in errors.password_repeat"
              :key="error"
              class="error"
            >
              {{ error }}
            </p>
          </div>
        </div>
      </div>

      <label class="policy">
        <input type="checkbox" name="policy" v-model="policy" />
        <p>
          Нажимая на кнопку “Регистрация”, я подтверждаю свое согласение с
          политикой конфиденциальности и обработки персональных данных
        </p>
      </label>

      <button type="submit" class="btn" :disabled="!policy">Регистрация</button>
    </div>
  </form>
</template>

<script>
import AppSwitcher from "./AppSwitcher.vue";

export default {
  name: "AppForm",
  components: { AppSwitcher },
  props: {
    defaultValues: Object,
    roles: Array,
    errors: Object,
  },
  data: function () {
    return {
      publicSwitcher: true,
      username: this.defaultValues.username ?? "",
      role: this.defaultValues.role ?? "",
      email: this.defaultValues.email ?? "",
      password: this.defaultValues.password ?? "",
      password_repeat: this.defaultValues.password_repeat ?? "",
      policy: true,
    };
  },
  methods: {
    sendForm() {
      const data = {
        public: this.publicSwitcher ? 1 : 0,
        username: this.username,
        role: this.role,
        email: this.email,
        password: this.password,
        password_repeat: this.password_repeat,
      };
      this.$emit("sendForm", data);
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 958px;
  margin: 0 auto;
}
.form__head {
  padding: 27px 20px;
  box-shadow: 0px -1px 0px 0px #edeff3 inset;
}
.form__title {
  font-size: 19px;
  font-weight: 700;
  line-height: 27px;
  letter-spacing: -0.0035em;
}
.form__body {
  padding: 27px 20px;
}
.public {
  display: flex;
  flex-direction: column;
  gap: 15px;
  padding-bottom: 30px;
  border-bottom: 1px solid #d9d9d9;
}
.public__label {
  display: flex;
  gap: 15px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 500;
  line-height: 19px;
}
.public__desc {
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.0015em;
  color: #696977;
}
.form__subtitle {
  font-size: 16px;
  font-weight: 500;
  line-height: 19px;
}
.data {
  padding: 20px 0 30.5px;
  border-bottom: 1px solid #d9d9d9;
}
.data__row {
  display: flex;
  gap: 18px;
  margin-top: 25px;
}
.data__row > * {
  width: 50%;
}
.input {
  width: 100%;
  padding: 10px;
  border: 1px solid #e6e6eb;
  border-radius: 11px;
  box-sizing: border-box;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.0015em;
}
.policy {
  display: flex;
  align-items: flex-start;
  gap: 15px;
  padding: 25px 0 30px;
  max-width: 682px;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.0015em;
  cursor: pointer;
}
.btn {
  display: block;
  margin: 0 auto;
  min-width: 234px;
  padding: 10px 12px;
  border: 1px solid #07a86e;
  border-radius: 9px;
  background-color: #fff;
  color: #07a86e;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.0015em;
  text-align: center;
  cursor: pointer;
  transition: 0.3s;
}
.btn:not([disabled]):hover {
  background-color: #07a86e;
  color: #fff;
}
.btn[disabled] {
  opacity: 0.5;
  cursor: not-allowed;
}
.error {
  color: red;
  font-size: 12px;
  margin-left: 10px;
  margin-top: 2px;
}
</style>
