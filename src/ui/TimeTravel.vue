<template>
  <div class="card-header">
    <div class="">
      <div class="input-group">
        <span class="input-group-text">Gestation</span>
        <input type="number" class="form-control" v-model="minggu" />
        <span class="input-group-text">Week</span>
        <input type="number" class="form-control" v-model="hari" />
        <span class="input-group-text">Day</span>
      </div>
      <div class="d-inline-flex mt-1">
        <h5 class="my-auto me-1">on</h5>
        <input class="form-control" type="date" v-model="date" />
        <button
          type="button"
          class="my-auto btn btn-sm btn-outline-primary"
          @click="resetForm"
        >
          <i class="fas fa-sync"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";

export default {
  props: ["lmpDate"],
  data() {
    const minggu = 0;
    const hari = 0;
    const date = dayjs().format("YYYY-MM-DD");

    return {
      minggu,
      hari,
      date,
    };
  },
  methods: {
    resetForm() {
      this.minggu = 0;
      this.hari = 0;
      this.date = this.lmpDate;
    },
    mingguHari() {
      const inputDate = dayjs(this.date);
      const lmp = dayjs(this.lmpDate);
      const delta = inputDate.diff(lmp, "day");
      this.minggu = Math.floor(delta / 7);
      this.hari = delta % 7;
    },
    targetDate() {
      const lmp = dayjs(this.lmpDate);
      const target = lmp
        .add(this.minggu, "week")
        .add(this.hari, "day")
        .format("YYYY-MM-DD");
      this.date = target;
    },
  },
  computed: {
    resultDate() {
      const lmp = dayjs(this.lmpDate);
      const result = lmp.add(this.minggu, "week").add(this.hari, "day");
      return result.format("YYYY-MM-DD");
    },
  },
  watch: {
    date() {
      this.mingguHari();
    },
    minggu() {
      this.targetDate();
    },
    hari() {
      this.targetDate();
    },
  },
};
</script>