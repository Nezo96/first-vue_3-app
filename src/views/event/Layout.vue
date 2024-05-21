<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'

const props = defineProps({
  id: {
    required: true,
  },
})

const event = ref(null)

onMounted(() => {
  // Fetch event by id and set local data
  EventService.getEvent(props.id)
    .then((response) => {
      event.value = response.data
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<template>
  <div v-if="event">
    <!--display single event data-->
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <!--/event/2-->
      <router-link :to="{ name: 'event-details' }">Details</router-link>
      <!--/event/2/register-->
      <router-link :to="{ name: 'event-register' }">Register</router-link>
      <!--/event/2/edit-->
      <router-link :to="{ name: 'event-edit' }">Edit</router-link>
    </div>
    <router-view :event="event" />
  </div>
</template>
