<template>
  <div class="my-1">
    <fieldset class="">
      <div class="row gx-0 justify-content-center">
        <label
          class="col-2 col-form-label"
          :for="jenisTarikh"
          :id="jenisTarikh"
          >{{ jenisTarikh }}</label
        >
        <div class="col-6">
          <input
            class="form-control"
            type="date"
            :name="jenisTarikh"
            :id="jenisTarikh"
            v-model="chosenDate.date"
          />
        </div>
        <span
          class="col-2 col-form-label"
          :for="jenisTarikh"
          :id="jenisTarikh"
          >{{ chosenDate.day }}</span
        >
      </div>
    </fieldset>
  </div>
</template>

<script>
import dayjs from "dayjs";

export default {
  props: ["jenisTarikh", "tarikh"],
  emits: ["date-string"],
  data() {
    const chosenDate = {
      date: this.tarikh,
      day: "",
      punca: this.jenisTarikh,
    };
    return {
      chosenDate,
    };
  },
  methods: {
    hariString() {
      return dayjs(this.chosenDate.date).format("ddd");
    },
  },
  watch: {
    "chosenDate.date": function () {
      this.chosenDate.day = this.hariString();
      this.$emit("date-string", this.chosenDate);
    },
    tarikh() {
      this.chosenDate.date = this.tarikh;
    },
  },
};
</script>
