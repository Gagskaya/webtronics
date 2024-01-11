<script setup lang="js">
import {API_URL} from '../constants';

const state = reactive({
  tickets : []
});

const router = useRouter();


const {data} = await useFetch(`${API_URL}/users/1?_embed=tickets`);
state.tickets = data.value?.tickets;

onMounted(() => {
  const token = localStorage?.getItem('token');

  if(!token) {
    router.push('login');
  };
})
</script>

<template>
  <div class="container">
    <Header />
    <div class="tickets">
      <table class="tickted">
        <tr>
          <th>Автор</th>
          <th>id</th>
          <th>Заголовок</th>
          <th>Сообщение</th>
          <th>Дата создания</th>
          <th></th>
        </tr>
        <tr v-for="item in state.tickets" :key="item.id">
          <td>
            <NuxtLink to="profile">{{ item.author }}</NuxtLink>
          </td>
          <td>{{ item.id }}</td>
          <td>{{ item.title }}</td>
          <td>{{ item.description }}</td>
          <td>{{ item.created_at }}</td>
          <td><NuxtLink :to="`ticket/${item.id}`">Подробнее</NuxtLink></td>
        </tr>
      </table>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.container {
  width: 850px;
  margin: 0 auto;
}
table {
  margin-top: 30px;
  td,
  th {
    padding: 15px;
    border: 1px solid rgb(212, 211, 211);
    border-radius: 4px;
  }
}
</style>
