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
            class="btn btn-outline-primary me-2 position-relative"
            @click="buangBarisan(idx)"
          >
            {{ masaRekod }}
            <span class="position-absolute top-0 start-100 translate-middle">
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
  props: ["lmpDate"],
  data() {
    const hariIni = dayjs().format("dddd DD-MM-YYYY");
    const masaRekod = dayjs().format("hh:mm");
    const koleksi = ["23/45/2022"];
    return {
      hariIni,
      masaRekod,
      koleksi,
    };
  },
  methods: {
    buangBarisan(idx) {
      this.koleksi.splice(idx, 1);
    },
  },
  watch: {
    lmpDate(newDate, oldDate) {
      if (newDate === oldDate) return;
      this.koleksi.push(newDate);
    },
  },
};
</script>
<style scoped>
li::before {
  margin: auto;
}
</style>