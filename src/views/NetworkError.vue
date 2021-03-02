<template>
  <div>
    <h1>Network Issues</h1>
    <router-link :to="{ name: 'EventList' }">Back to home page</router-link>
    or
    <a href="#" @click="$router.go(-1)">retry</a>
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
