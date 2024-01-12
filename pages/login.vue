<script setup lang="js">
import {API_URL} from '../constants';

const router = useRouter();

const state = reactive({
  email : "",
  password : "",
  isVisiblePassword : false
});

const togglePasswordType = () => {
  state.isVisiblePassword = !state.isVisiblePassword;
}


const onSubmit = async () => {
  await useFetch(`${API_URL}/login`, {
    method : 'POST',
    body : {email : state.email, password : state.password},
    onResponse({_, response}) {
     const token = response._data.accessToken;
     localStorage.setItem('token', token);
     router.push('/');
    },
    onResponseError({_, response}) {
      alert(response._data)
    }
  });
}



onMounted(() => {
  const token = localStorage.getItem('token');
  if(token) {
    router.push('/');
  }
})
</script>
<template>
  <div class="container">
    <div class="login">
      <input
        placeholder="Ваш E-mail"
        class="login__input login__input-email"
        type="email"
        v-model="state.email"
      />
      <div class="login__input-wrap">
        <input
          placeholder="Пароль"
          class="login__input login__input-password"
          :type="state.isVisiblePassword ? 'text' : 'password'"
          v-model="state.password"
          @keydown.enter="onSubmit"
        />
        <font-awesome-icon
          icon="eye-slash"
          class="login__input-password-icon"
          v-show="state.isVisiblePassword"
          @click="togglePasswordType"
        />
        <font-awesome-icon
          icon="eye"
          class="login__input-password-icon"
          @click="togglePasswordType"
          v-show="!state.isVisiblePassword"
        />
      </div>

      <button
        class="login__btn"
        @click="onSubmit"
        :disabled="!state.email.length || !state.password.length"
      >
        Вход
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  width: 850px;
  margin: 0 auto;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.login {
  display: flex;
  flex-direction: column;
  &__input {
    display: inline-block;
    min-width: 290px;
    padding: 10px 15px;
    &-wrap {
      position: relative;
    }
    &-password {
      margin-top: 15px;
      margin-bottom: 15px;
      &-icon {
        position: absolute;
        top: 27px;
        right: 15px;
        cursor: pointer;
      }
    }
  }
  &__btn {
    padding: 15px;
    background: #005ff9;
    border: none;
    color: #fff;
    cursor: pointer;
    border-radius: 4px;

    &:hover {
      background-color: #111;
    }
    &:disabled {
      cursor: not-allowed;
      background-color: gray;
    }
  }
}
</style>
