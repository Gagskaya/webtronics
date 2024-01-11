<script setup lang="js">
import {API_URL} from '../../constants';

const route = useRoute();
const router = useRouter();

const state = reactive({
    ticket : {}
});

const {data} = await useFetch(`${API_URL}/tickets/${route.params.id}`);
state.ticket = data.value;

onMounted(() => {
  const token = localStorage?.getItem('token');

if(!token) {
  router.push('login');
}
});
</script>
<template>
  <div class="container">
    <Header />
    <p>Автор : {{ state.ticket.author }}</p>
    <p>id : {{ state.ticket.id }}</p>
    <p>Заголовок : {{ state.ticket.title }}</p>
    <p>Сообщение : {{ state.ticket.description }}</p>
    <p>Дата создания: {{ state.ticket.created_at }}</p>
  </div>
</template>

<style lang="scss" scoped>
.container {
  width: 850px;
  margin: 0 auto;
}
</style>
