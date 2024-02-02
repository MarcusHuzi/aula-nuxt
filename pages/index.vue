<template>
<div>
  <h1> Events </h1>
  <EventCard
    v-for="(event, index) in events"
    :key="index"
    :event="event"
    :data-index="index"
  />
</div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'

export default {
  name: 'IndexPage',
  components: {
    EventCard,
  },
  async fetch({ error, store }) {
    try {
      await store.dispatch('events/fetchEvents')

    } catch (e) {
      error({
        statusCode: 503,
        message: 'Não é possível resgatar eventos no momento, tente novamente.'
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
  computed: {
    ...mapState({
      events: state => state.events.events
    })
  },
}
</script>

