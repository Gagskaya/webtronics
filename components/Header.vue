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
    <button @click="onLogoutClick">Выйти</button>
  </header>
</template>

<style lang="scss" scoped>
.header {
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
}
</style>
