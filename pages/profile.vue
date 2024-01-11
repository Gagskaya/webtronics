<script setup lang="js">
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

const router = useRouter();

const state = reactive({
  user : {},
  date : '09.09.1976'
})

const {data} = await useFetch('http://127.0.0.1:3002/users/1?_embed=tickets');

state.user = data.value;

onMounted(() => {
  const token = localStorage?.getItem('token');

  if(!token) {
    router.push('login');
  }
})
</script>
<template>
  <div class="container">
    <Header />
    <div class="profile">
      <p>
        Имя и фамилия: {{ state.user?.firstName }} {{ state.user?.lastName }}
      </p>
      <p>Почта: {{ state.user?.email }}</p>
      <div style="display: flex; align-items: center">
        <p style="margin-right: 15px">День рождения:</p>
        <VueDatePicker v-model="state.date" style="width: 200px" />
      </div>

      <p>
        Город:
        <select name="city" id="city">
          <option>Москва</option>
          <option>Санкт-Петербург</option>
          <option>Таганрог</option>
        </select>
      </p>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.container {
  width: 850px;
  margin: 0 auto;
}
.profile {
  margin-top: 30px;
}
</style>
