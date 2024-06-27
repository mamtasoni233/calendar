<template>
  <div class="container">
    <div class="row">
      <div class="col-md-4">
        <select class="form-select" aria-label="Default select example">
          <!-- <option selected>Open this select menu</option> -->
          <option value="selected">Select Month</option>
          <option value="2">Select Week</option>
          <option value="3">Select Day</option>
        </select>
      </div>
    </div>

    <!--  <FullCalendar :initialView="initialView" /> -->
  </div>
</template>
<script>
/* import FullCalendar from "@fullcalendar/vue3"; */
/* import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
import timeGridPlugin from "@fullcalendar/timegrid"; */
export default {
  name: "FullCalendar",
  data() {
    return {
      /* calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin, timeGridPlugin],
      }, */
    };
  },
  /*   props: {
    initialViews: {
      type: String,
      default: "dayGridMonth",
    },
  }, */
};
</script>
