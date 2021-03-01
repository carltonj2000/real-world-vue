<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>@ {{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script>
import EventService from '../services/EventService'

export default {
  name: 'EventDetails',
  props: {
    id: String
  },
  data() {
    return {
      event: null
    }
  },
  async created() {
    try {
      const response = await EventService.getEvent(this.id)
      this.event = response.data
    } catch (e) {
      console.log(e)
    }
  }
}
</script>
