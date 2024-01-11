<script setup lang="js">
const route = useRoute();

const state = reactive({
    ticket : {}
})

const {data} = await useFetch(`http://127.0.0.1:3002/tickets/${route.params.id}`);
state.ticket = data.value
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
