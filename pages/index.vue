<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'

export default {
  head() {
    // <-- property used by vue-meta to add header tags
    return {
      title: 'Event Listing' // <-- For our title tag
    }
  },
  //asyncData life hook is called every time before loading a page component
  //it will be called server-side once (on the first request to the Nuxt app) and client-side when navigating to further routes
  //this method receives the context as the first argument
  // asyncData(context) {
  //   return context.$axios.get('http://localhost:3000/events').then(response => {
  //     return {
  //       events: response.data
  //     }
  //   })
  //   .catch(e => {
  //   error({
  //     statusCode: 503,
  //     message: 'Unable to fetch events at this time, please try again'
  //   })
  // })
  // },
  //using ES6 destructuring the context object we can take out just the modules we need
  async asyncData({ $axios, error }) {
    try {
      // const response = await $axios.get('http://localhost:3000/events')
      // return {
      //   events: response.data
      // }
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events events at this time'
      })
    }
  },
  components: {
    EventCard
  }
}
</script>
