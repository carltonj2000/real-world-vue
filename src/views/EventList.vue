<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <div class="pagination">
      <router-link
        v-if="page - 1 > 0"
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        rel="prev"
      >
        &lt;&lt; Page {{ page - 1 }}
      </router-link>
      <router-link
        v-if="hasNextPage"
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        rel="next"
      >
        Page {{ page + 1 }} &gt;&gt;
      </router-link>
    </div>
  </div>
</template>

<script>
import { watchEffect } from 'vue'
import EventCard from '@/components/EventCard.vue'
import EventService from '../services/EventService'

export default {
  name: 'EventList',
  props: {
    page: Number,
    perPage: Number
  },
  components: {
    EventCard
  },
  data() {
    return {
      events: null,
      totalEvents: 0
    }
  },
  async created() {
    watchEffect(async () => {
      this.events = null
      try {
        const response = await EventService.getEvents(this.perPage, this.page)
        this.events = response.data
        this.totalEvents = response.headers['x-total-count']
      } catch (e) {
        console.log(e)
      }
    })
  },
  computed: {
    hasNextPage() {
      return this.page < Math.ceil(this.totalEvents / 2)
    }
  }
}
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  justify-content: space-between;
  width: 290px;
}
.pagination a {
  text-decoration: none;
  color: #2c3e50;
}
</style>
