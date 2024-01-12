<script lang="js" setup>
const router = useRouter();

const onLogoutClick = () => {
  router.push('/login');
  localStorage.removeItem('token');
};
</script>
<template>
  <header class="header">
    <NuxtLink to="/" class="header__link">Главная</NuxtLink>
    <NuxtLink to="profile" class="header__link">Профиль</NuxtLink>
    <button class="header__logout" @click="onLogoutClick">Выйти</button>
  </header>
</template>

<style lang="scss" scoped>
.header {
  display: flex;
  align-items: center;
  &__link {
    font-size: 20px;
    margin-right: 15px;
    color: gray;
    text-decoration: none;
    &:hover {
      text-decoration: underline;
      color: rgb(61, 61, 236);
    }
  }
  &__logout {
    border: none;
    color: #fff;
    background-color: #2b3bc7;
    border-radius: 4px;
    padding: 10px;
    cursor: pointer;
    &:hover {
      background-color: #111;
    }
  }
}
</style>
