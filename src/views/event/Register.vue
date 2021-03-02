<template>
  <div v-if="event">
    <p>Register for the event</p>
    <button @click="register">Register Me</button>
  </div>
</template>

<script>
export default {
  props: ['event'],
  methods: {
    register() {
      // call api
      //this.$router.push({ name: 'EventDetails', params: { id: this.event.id } })
      this.$router.push({ name: 'EventDetails' })
    }
  }
}
</script>
