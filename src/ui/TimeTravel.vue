<template>
  <div class="card-header">
    <div class="form">
      <div class="input-group">
        <span class="input-group-text">Gestation</span>
        <input type="number" class="form-control" v-model="minggu" />
        <span class="input-group-text">Week</span>
        <input type="number" class="form-control" v-model="hari" />
        <span class="input-group-text">Day</span>
      </div>
      <div class="input-group">
        <span class="input-group-text">is on</span>
        <input
          type="text"
          class="form-control text-center fw-bold"
          readonly
          :value="resultDate"
        />
        <button
          type="button"
          class="btn btn-outline-secondary"
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

    return {
      minggu,
      hari,
    };
  },
  methods: {
    resetForm() {
      this.minggu = 0;
      this.hari = 0;
    },
  },
  computed: {
    resultDate() {
      const lmp = dayjs(this.lmpDate);
      const result = lmp.add(this.minggu, "week").add(this.hari, "day");
      return result.format("DD-MM-YYYY");
    },
  },
};
</script>