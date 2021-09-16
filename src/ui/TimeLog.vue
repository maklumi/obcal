<template>
  <div class="card mb-3">
    <div class="card-header fw-bold">{{ hariIni }}</div>
    <div class="card-body p-0">
      <ol class="list-group list-group-numbered">
        <li
          class="list-group-item d-flex justify-content-between"
          v-for="(item, idx) in koleksi"
          :key="idx"
        >
          <button
            class="btn btn-outline-primary me-2 d-inline-flex"
            @click="buangBarisan(idx)"
          >
            {{ masaRekod }}
            <span class="ms-2">
              <i class="fas fa-times-circle"></i>
            </span>
          </button>

          <input
            type="text"
            class="form-control text-center"
            readonly
            :value="item"
          />
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";
export default {
  props: ["date", "weekDay"],
  data() {
    const hariIni = dayjs().format("dddd DD-MM-YYYY");
    const masaRekod = dayjs().format("hh:mm");
    const koleksi = [];
    const clocked = dayjs();
    return {
      hariIni,
      masaRekod,
      koleksi,
      clocked,
    };
  },
  methods: {
    buangBarisan(idx) {
      this.koleksi.splice(idx, 1);
    },
  },
  watch: {
    weekDay(wd, old) {
      if (wd === old) return;
      const now = dayjs();
      if (now.diff(this.clocked, "second") < 5) return;
      this.clocked = now;
      const teks = "LMP " + this.date + " " + wd.week + "+" + wd.day + "/7";
      this.koleksi.push(teks);
    },
  },
};
</script>
<style scoped>
li::before {
  margin: auto;
}
</style>