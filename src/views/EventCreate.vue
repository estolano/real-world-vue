<template>
  <div>
    <h1>Create an Event, {{ user.name }}</h1>
    <p>This event is created by {{ user.name }}, {{ catLength }} categories.</p>
    <ul>
      <li v-for="cat in categories" :key="cat">{{ cat }}</li>
    </ul>
    <p>Event #1 is {{ getEventById(1) }} .</p>
    <p></p>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  computed: {
    catLength() {
      return this.$store.getters.catLength
    },

    localComputed() {
      return 'something'
    },
    ...mapGetters(['getEventById']),
    ...mapState(['categories', 'user']) // <-- using object spread operator
  }
}
</script>
<style scoped></style>
