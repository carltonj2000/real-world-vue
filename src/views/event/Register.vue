<template>
  <div v-if="event">
    <p>Register for the event</p>
    <button @click="register">Register Me</button>
  </div>
</template>

<script>
export default {
  props: ['event'],
  inject: ['GStore'],
  methods: {
    register() {
      // call api
      //this.$router.push({ name: 'EventDetails', params: { id: this.event.id } })
      this.GStore.flashMessage = 'You are registered for ' + this.event.title
      setTimeout(() => (this.GStore.flashMessage = ''), 3000)
      this.$router.push({ name: 'EventDetails' })
    }
  }
}
</script>
