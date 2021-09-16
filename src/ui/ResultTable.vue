<template>
  <div class="card card-header">
    <table class="table table-danger table-striped">
      <tbody>
        <satu-item weekNumber="week 14" :dateValue="dateValues.week14" />
        <satu-item weekNumber="week 20" :dateValue="dateValues.week20" />
        <satu-item weekNumber="week 28" :dateValue="dateValues.week28" />
        <satu-item weekNumber="week 38" :dateValue="dateValues.week38" />
      </tbody>
    </table>
  </div>
</template>

<script>
import SatuItem from "../components/SatuItem.vue";
import dayjs from "dayjs";

export default {
  components: { SatuItem },
  props: ["lmpDate"],
  methods: {
    setWeek(num) {
      const tempLmp = dayjs(this.lmpDate.date).add(num, "week");
      return tempLmp.format("DD-MM-YYYY");
    },
  },
  computed: {
    dateValues() {
      return {
        week14: this.setWeek(14),
        week20: this.setWeek(20),
        week28: this.setWeek(28),
        week38: this.setWeek(38),
      };
    },
  },
};
</script>