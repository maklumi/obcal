<template>
  <div class="container">
    <satu-kad
      jenis-tarikh="lmp"
      @date-string="dariLmp"
      :tarikh="lmpDate.date"
    ></satu-kad>
    <satu-kad
      jenis-tarikh="due"
      @date-string="dariEdd"
      :tarikh="eddDate.date"
    ></satu-kad>
    <result-table :lmpDate="lmpDate" />
    <div class="card">
      <p>lmp {{ lmpDate }}</p>
      <p>edd {{ eddDate }}</p>
    </div>
  </div>
</template>

<script>
import dayjs from "dayjs";
import localizedFormat from "dayjs/plugin/localizedFormat";
import SatuKad from "./components/SatuKad.vue";
import ResultTable from "./ui/ResultTable.vue";

export default {
  components: { SatuKad, ResultTable },
  data() {
    dayjs.locale("my");
    dayjs.extend(localizedFormat);
    const lmpDate = {
      date: dayjs().format("YYYY-MM-DD"),
    };
    const eddDate = {
      date: dayjs().add(40, "week").format("YYYY-MM-DD"),
    };

    return {
      lmpDate,
      eddDate,
    };
  },
  methods: {
    dariLmp(obj) {
      // console.log(obj.punca, obj.date, obj.day);
      this.lmpDate.date = obj.date;
      this.setWeek40();
    },
    dariEdd(obj) {
      this.eddDate.date = obj.date;
      this.setWeek0();
    },
    setWeek40() {
      const temp = dayjs(this.lmpDate.date).add(40, "week");
      this.eddDate.date = temp.format("YYYY-MM-DD");
    },
    setWeek0() {
      const tempLmp = dayjs(this.eddDate.date).subtract(40, "week");
      this.lmpDate.date = tempLmp.format("YYYY-MM-DD");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 1rem;
}
</style>
