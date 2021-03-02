<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails' }"> Details </router-link>
      |
      <router-link :to="{ name: 'EventRegister' }"> Register </router-link>
      |
      <router-link :to="{ name: 'EventEdit' }"> Edit </router-link>
      <router-view :event="event" />
    </div>
  </div>
</template>

<script>
import EventService from '../../services/EventService'

export default {
  name: 'Details',
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
    } catch (error) {
      console.log({ error })
      if (error.response && error.response.status === 404) {
        this.$router.push({ name: '404', params: { resource: 'Event' } })
      } else {
        this.$router.push({ name: 'NetworkError' })
      }
    }
  }
}
</script>
