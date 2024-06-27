<template>
  <div>
    <!-- <FullCalendar /> -->
    <!--   <HelloWorld />
  <HelloWorld initialView="dayGridMonth" headerList="dayGridMonth" />
  <HelloWorld initialView="dayGridDay" headerList="dayGridDay" />
  <HelloWorld initialView="dayGridWeek" headerList="dayGridWeek" /> -->
    <!--  <dayCal />
  <monthCal />
  <weekCal /> -->
    <HelloWorld />
  </div>
</template>

<script>
/* import HelloWorld from "./components/HelloWorld.vue"; */
import HelloWorld from "./components/HelloWorld.vue";
/* import FullCalendar from "./components/FullCalendar.vue"; */
/*import monthCal from "./components/monthCal.vue";
import HelloWorld from "./components/HelloWorld.vue"; */

export default {
  name: "App",
  components: {
    HelloWorld,
    /*   FullCalendar, */
    /*  dayCal,
    monthCal,
    weekCal, */
  },
};
</script>
