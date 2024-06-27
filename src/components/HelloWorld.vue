<template>
  <div class="container">
    <h1 class="text-center">Vue-Calendar</h1>
    <div class="row">
      <!-- <FullCalendar /> -->
      <!-- <div class="col-md-3">
        <button class="btn btn-outline-primary" @click="loadFullCalendar">
          Load Component A
        </button>
      </div> -->
      <div class="text-center col-md-4"></div>
      <div class="text-center col-md-4">
        <select
          class="form-select"
          aria-label="Default select example"
          v-model="selected"
        >
          <option
            v-for="option in options"
            :value="option.value"
            :key="option.value"
          >
            {{ option.name }}
          </option>
        </select>
      </div>
      <FullCalendar :initialView="selected" />
      <!-- <Calendar  /> -->
      <!-- <FullCalendar v-if="HideFullCalendar" />-->
      <FullCalendar initialView="dayGridMonth" headerList="dayGridMonth" />
      <FullCalendar initialView="dayGridDay" headerList="dayGridDay" />
      <FullCalendar initialView="timeGridWeek" headerList="timeGridWeek" />
      <!--  <dayCal />
      <monthCal />
      <weekCal /> -->
    </div>
  </div>
</template>

<script>
import FullCalendar from "./FullCalendar.vue";
// import Calendar from "./monthCal.vue";
/* import FullCalendar from "./components/FullCalendar.vue"; */
/*import monthCal from "./components/monthCal.vue";
import weekCal from "./components/weekCal.vue"; */

export default {
  name: "weekCal",
  data() {
    return {
      // showFullCalendar: false,
      // HideFullCalendar: true,
      selected: "dayGridWeek",
      options: [
        { value: "dayGridWeek", name: "Week" },
        { value: "dayGridDay", name: "Day" },
        { value: "dayGridMonth", name: "Month" },
      ],
      initialView: "",
    };
  },
  components: {
    FullCalendar,
    // Calendar,
    /*   FullCalendar, */
    /*  dayCal,
    monthCal,
    weekCal, */
  },
  methods: {
    // loadFullCalendar() {
    //   // Set showFullCalendar to true to render the FullCalendar component
    //   this.showFullCalendar = !this.showFullCalendar;
    //   this.HideFullCalendar = !this.HideFullCalendar;
    // },
  },
};
</script>
