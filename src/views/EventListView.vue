<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import EventCard from "@/components/EventCard.vue"; // @ is an alias to /src
import * as EventService from "@/services/EventServices";
export default defineComponent({
  name: "EventListView",
  components: {
    EventCard,
  },
  data() {
    return { events: null };
  },
  created() {
    EventService.getEvents()
      .then((response) => {
        this.events = response.data;
      })
      .catch((err) => {
        console.log(err);
      });
  },
});
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
