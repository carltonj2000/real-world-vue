<template>
  <div>
    <h1>{{ resource }} Not Found</h1>
    <router-link :to="{ name: 'EventList' }">Back to home page</router-link>
  </div>
</template>

<script>
export default {
  props: {
    resource: {
      type: String,
      default: 'Page'
    }
  }
}
</script>
