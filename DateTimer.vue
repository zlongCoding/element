
<template>
  <div>
    <el-date-picker
      v-model="value1"
      type="datetime"
      :popper-class="`date-picker-hard-code ${resetclassNames}`"
      format="yyyy-MM-dd HH:mm"
      @focus="timerfocus"
      @change="timerchange"
      placeholder="选择日期时间"
    >
    </el-date-picker>
  </div>
</template>

<script>
export default {
  methods: {
    renderTimerLists() {
      let timeArray = [];
      let html = ``;
      let classNames = `time-select-item render-hardcode-Lists ${this.resetclassNames}`;
      for (let i = 0; i < 24; i++) {
        for (let j = 0; j < 2; j++) {
          timeArray.push(
            `${i < 10 ? `0${i}` : `${i}`}:${j == 0 ? "00" : "30"}`
          );
          html += `<div class='${classNames}'>${i < 10 ? `0${i}` : `${i}`}:${
            j == 0 ? "00" : "30"
          }</div>`;
        }
      }
      html += `<div class='${classNames}'>24:00</div>`;
      return html;
    },
    timerfocus() {
      if (this.loaded) {
        return;
      }
      this.loaded = true;
      setTimeout(() => {
        let wrapper = document.getElementsByClassName(this.resetclassNames)[0];
        let date = wrapper.getElementsByClassName("el-time-panel")[0];
        date.innerHTML = `<div class="reset-timer-codes"><div><div><div>${this.renderTimerLists()}</div></div><div class="el-scrollbar__bar is-horizontal"><div class="el-scrollbar__thumb" style="transform: translateX(0%);"></div></div><div class="el-scrollbar__bar is-vertical"><div class="el-scrollbar__thumb" style="height: 13.5501%; transform: translateY(571.5%);"></div></div></div></div>`;
      }, 0);
    },
    timerchange() {
      if (!this.value1) {
        this.value1 = null
        return
      }
      let times = this.timeValue.split(":");
      let val = this.value1;
      let values = new Date(
        val.getFullYear(),
        val.getMonth(),
        val.getDate(),
        Number(times[0]),
        Number(times[1])
      ).getTime();
      this.$emit("onTime", values);
    },

    listener(e) {
      if (e.target.classList.contains(this.resetclassNames)) {
        this.timeValue = e.target.innerText;
        this.timerchange();
      }
    },
  },
  props: {
    dateTime: {
      type: Number | String,
      default: new Date().getTime(),
    },
    step: {
      type: Number,
      default: 30,
    },
  },
  watch: {
    dateTime(val) {
      if (val) {
        this.value1 = new Date(val);
      }
      
    },
  },
  mounted() {
    window.addEventListener("click", this.listener, true);
  },
  beforeDestroy() {
    window.addEventListener("click", this.listener, true);
  },
  data() {
    return {
      resetclassNames: `date-picker-hard-code${this._uid}`,
      value1: new Date(),
      loaded: false,
      timeValue: ":",
    };
  },
};
</script>
<style  lang="scss">
</style>