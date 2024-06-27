<template>
  <div class="container">
    <div class="hello">
      <!--  <button @click="toggleWeekends">toggle weekends</button> -->
      <FullCalendar
        ref="fullCalendar"
        :options="calendarOptions"
        :events="events"
      />
    </div>
  </div>
</template>

<script>
import FullCalendar from "@fullcalendar/vue3";
import axios from "axios";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
import timeGridPlugin from "@fullcalendar/timegrid";
// import { INITIAL_EVENTS, createEventId } from "../events";
export default {
  name: "App",
  data() {
    return {
      AddEvent: false,
      showFullCalendar: false,
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin, timeGridPlugin],
        headerToolbar: {
          left: "prev,next today",
          center: "title",
          right: this.headerList,
        },
        events: [],
        initialView: this.initialView,
        // initialEvents: INITIAL_EVENTS, // alternatively, use the `events` setting to fetch from a feed
        editable: true,
        selectable: true,
        selectMirror: true,
        dayMaxEvents: true,
        weekends: true,
        select: this.handleDateSelect,
        eventClick: this.handleEventClick,
        eventsSet: this.handleEvents,
        event: {
          eventDate: "",
          eventtype: "",
        },
      },
    };
  },
  mounted() {
    this.getEvents();
  },
  components: {
    FullCalendar,
  },
  props: {
    initialView: {
      type: String,
      default: "dayGridMonth",
    },
    headerList: {
      type: String,
      default: "dayGridMonth,timeGridWeek,dayGridDay",
    },
  },
  watch: {
    initialView() {
      let calendarApi = this.$refs.fullCalendar;
      calendarApi.getApi().changeView(this.initialView);
      this.calendarOptions.headerToolbar.right = this.headerList;
    },
  },
  methods: {
    handleDateClick: function (arg) {
      alert("date click! " + arg.dateStr);
    },
    toggleWeekends: function () {
      this.calendarOptions.weekends = !this.calendarOptions.weekends; // toggle the boolean!
    },
    handleWeekendsToggle() {
      this.calendarOptions.weekends = !this.calendarOptions.weekends; // update a property
    },
    handleDateSelect(selectInfo) {
      let title = prompt("Please enter a new title for your event");
      let calendarApi = selectInfo.view.calendar;
      calendarApi.unselect(); // clear date selection

      if (title) {
        calendarApi.addEvent({
          // id: createEventId(),
          title,
          start: selectInfo.startStr,
          end: selectInfo.endStr,
          allDay: selectInfo.allDay,
        });
        console.log("selectInfo", selectInfo);
        this.event = {
          eventDate: selectInfo.startStr,
          eventtype: title,
        };

        axios.post("http://127.0.0.1:53414/event/addEvent", this.event);
      }
    },
    handleEventClick(clickInfo) {
      console.log("clickInfo", clickInfo.event.id);
      if (
        confirm(
          `Are you sure you want to delete the event '${clickInfo.event.title}'`
        )
      ) {
        axios.delete(
          "http://127.0.0.1:53414/event/deleteEvent/id/" + clickInfo.event.id
        );
        clickInfo.event.remove();
        this.getEvents();
      }
    },
    handleEvents(events) {
      this.currentEvents = events;
    },
    async getEvents() {
      let result = await axios.get("http://127.0.0.1:53414/event/getAllEvents");
      var eventArr = [];
      Array.from(result.data).forEach((value) => {
        var struct = {};
        struct = {
          id: value.id,
          title: value.eventtype,
          start: value.eventDate,
          end: value.endStr,
          allDay: true,
        };
        eventArr.push(struct);
      });
      this.calendarOptions.events = eventArr;
    },
  },
};
</script>
