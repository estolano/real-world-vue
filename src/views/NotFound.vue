<template>
  <div>
    <h1>Não encontrado {{ resource }}!!</h1>
    <router-link :to="{ name: 'event-list' }">volta para a lista</router-link>
  </div>
</template>

<script>
export default {
  props: {
    resource: {
      type: String,
      required: true
    }
  }
}
</script>
