<template>
  <div v-if="seconds" class="flex content-center justify-center mt-5">
    <div id="countdown-box">
      <div class="text-5xl">Countdown to: </div>
      <div class="text-4xl">{{endDate | formatDate}}</div>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{days | formatNum}}
        <div class="label text-sm absolute bottom-0">days</div>
      </div>
      <span class="mb-3">:</span>
      <div class="hours mx-2 relative">
        {{hours | formatNum}}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
      <span>:</span>
      <div class="minutes mx-2 relative">
        {{minutes | formatNum}}
        <div class="label text-sm absolute bottom-0">minutes</div>
      </div>
      <span>:</span>
      <div class="seconds ml-2 relative">
        <div>{{seconds | formatNum}}</div>
        <div class="label text-sm absolute bottom-0">seconds</div>
      </div>
    </section>
  </div>
  </div>
</template>
<script>
export default {
  name: 'Countdown',
  props: ["endDate"],
  data: () => ({
    days: null,
    hours: null,
    minutes: null,
    seconds: null
  }),
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60
    },
    _hours() {
      return this._minutes * 60
    },
    _days() {
      return this._hours * 24
    },
  },
  methods: {
    showRemaining() {
      console.log(this.endDate.toString())
      const timer = setInterval(() => {
        const now = new Date();
        const end = this.endDate;
        const distance = end.valueOf() - now.valueOf();

        if (distance < 0) {
          clearInterval(timer);
          return
        }
        const days = Math.floor((distance / this._days));
        const hours = Math.floor((distance % this._days) / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);

        this.days = days;
        this.hours = hours;
        this.minutes = minutes;
        this.seconds = seconds;

      }, 1000)
    }
  },
  mounted() {
    this.showRemaining();
  },
  filters: {
    formatNum: num => num < 10 ? "0" + num : num,
    formatDate: date => `${date.getDate()}-${date.getMonth() + 1}-${date.getFullYear()}`
  }
}
</script>

<style scoped>

.seconds {
  max-width: 60px;
}

#countdown-box {
  box-shadow: -4px -1px 25px 0 rgb(210, 210, 210);
  padding: 20px;
  align-self: center;
  width: 500px;
}
</style>
