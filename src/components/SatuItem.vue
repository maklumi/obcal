<template>
  <tr>
    <div class="row">
      <label for="week20" class="col-5 col-form-label">{{ weekNumber }}</label>
      <div class="col-5">
        <input
          type="text"
          class="form-control text-center"
          readonly
          :value="dateValue"
        />
      </div>
    </div>
  </tr>
</template>

<script>
export default {
  props: {
    weekNumber: {
      type: String,
      required: false,
      default: "Tajuk",
    },
    dateValue: {
      type: String,
      default: "00/00/0000",
    },
  },
};
</script>