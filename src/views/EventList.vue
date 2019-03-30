<template>
  <div>
    <h1>Events for {{ user.user.name }}</h1>
    <EventCard v-for="event in event.events" :key="event.id" :event="event" />
    <template v-if="page != 1">
      <router-link
        :to="{ name: 'event-list', query: { page: page - 1 } }"
        rel="prev"
        >Prev Page</router-link
      >|
    </template>
    <template v-if="page < lastPage">
      <router-link
        :to="{ name: 'event-list', query: { page: page + 1 } }"
        rel="next"
        >Next Page</router-link
      >
    </template>
  </div>
</template>
<script>
import EventCard from '@/components/EventCard.vue'
import { mapState } from 'vuex'
import store from '@/store/store'

function getPageEvents(routeTo, next) {
  const currentPage = parseInt(routeTo.query.page) || 1
  store
    .dispatch('event/fetchEvents', {
      page: currentPage
    })
    .then(() => {
      routeTo.params.page = currentPage
      next()
    })
}

export default {
  props: {
    page: {
      type: Number,
      required: true
    }
  },
  components: {
    EventCard
  },
  beforeRouteEnter(routeTo, routeFrom, next) {
    console.log('beforeRouteEnter')
    getPageEvents(routeTo, next)
  },
  beforeRouteUpdate(routeTo, routeFrom, next) {
    console.log('beforeRouteUpdate')
    getPageEvents(routeTo, next)
  },
  // created() {
  //   this.$store.dispatch('event/fetchEvents', {
  //     perPage: 3, // <-- How many items to display per page
  //     page: this.page // <-- What page we're on
  //   })
  // },
  computed: {
    lastPage() {
      return Math.ceil(this.event.eventsTotal / this.event.perPage)
    },
    ...mapState(['event', 'user'])
  }
}
</script>
