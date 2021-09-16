<template>
  <div class="card mb-3">
    <div class="card-header">Hari ini {{ todayStr }}</div>
    <div class="card-body">
      <div class="m">
        <h2 class="d-inline-flex">
          <span class="badge bg-secondary my-auto">{{ gestation.week }} </span>
          <p class="my-auto mx-1">
            {{ noEs(gestation.week) ? "week" : "weeks" }}
          </p>
          <span class="badge bg-secondary my-auto">{{ gestation.day }}</span>
          <p class="my-auto mx-1">{{ noEs(gestation.day) ? "day" : "days" }}</p>
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";
export default {
  props: ["lmpDate"],
  emits: ["weekDay"],
  data() {
    const todayStr = dayjs().format("DD-MM-YYYY");
    return {
      todayStr,
    };
  },
  methods: {
    noEs(num) {
      return num === 0 || num === 1 || num === -1;
    },
  },
  computed: {
    gestation() {
      const lmp = dayjs(this.lmpDate);
      const todayTemp = dayjs().format("YYYY-MM-DD");
      const today = dayjs(todayTemp);
      const diffDays = today.diff(lmp, "day");

      const week = Math.floor(diffDays / 7);
      const day = diffDays % 7;

      this.$emit("weekDay", { week, day });
      return {
        week,
        day,
      };
    },
  },
};
</script>