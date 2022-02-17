<template>
  <div class="intro">
    <img class="shark-race-logo" :src="require(`assets/img/logos/shark_race_club.svg`)" alt="">
    <div class="intro__container">
      <h2 class="intro__title">Sharkcoin</h2>
      <div class="sharkcoin-ido">
        <CoinSVG class="sharkcoin-ido__coin"/>
        <div class="sharkcoin-ido__wrapper">
        <h3 class="sharkcoin-ido__title">Sharkcoin (SHRK) IDO</h3>
        <div class="day-counter">
          <div class="day-counter__item" v-for="time in times">
            <div class="day-counter__num">{{ time.time }}</div>
            <div class="day-counter__text">{{ time.text }}</div>
          </div>
        </div>
          <div class="join">
            <h3 class="join__title">You can join and buy Sharkcoins  by using:</h3>
            <div class="join__buttons">
              <button class="button button__metamask">
                <img :src="require('assets/img/fox.svg')" class="button__metamask-img" alt="">
                Metamask
              </button>
              <button class="button button__connect">wallet connect</button>
            </div>
          </div>
      </div>
      </div>
    </div>
  </div>
</template>

<script>
import CoinSVG from "~/components/SVG/CoinSVG";
export default {
  name: "Intro",
  components: {CoinSVG},
  data() {
    return {
      startTime: "July 7, 2022 12:03:00",
      endTime: "March 20, 2022 10:47:00",
      times: [
        { id: 0, text: "Days", time: 1 },
        { id: 1, text: "Hours", time: 1 },
        { id: 2, text: "Minutes", time: 1 },
        { id: 3, text: "Seconds", time: 1 }
      ],
      progress: 100,
      timeinterval: undefined
    }
  },
  created() {
    this.updateTimer();
    this.timeinterval = setInterval(this.updateTimer, 1000);
  },
  methods: {
    updateTimer: function() {
      if (
        this.times[3].time > 0 ||
        this.times[2].time > 0 ||
        this.times[1].time > 0 ||
        this.times[0].time > 0
      ) {
        this.getTimeRemaining();
        this.updateProgressBar();
      } else {
        clearTimeout(this.timeinterval);
        // this.times[3].time = this.times[2].time = this.times[1].time = this.times[0].time = 0;
        this.progress = 0;
      }
      this.times.forEach((time)=> {
        if (time.time < 10) {
          time.time = '0' + time.time
        }
      })
    },
    getTimeRemaining: function() {
      let t = Date.parse(new Date(this.endTime)) - Date.parse(new Date());
      if(t >= 0){
        this.times[3].time = Math.floor(t / 1000 % 60); //seconds
        this.times[2].time = Math.floor(t / 1000 / 60 % 60); //minutes
        this.times[1].time = Math.floor(t / (1000 * 60 * 60) % 24); //hours
        this.times[0].time = Math.floor(t / (1000 * 60 * 60 * 24)); //days
      }
      else {
        this.times[3].time = this.times[2].time = this.times[1].time = this.times[0].time = 0;
        this.progress = 0;
      }
    },
    updateProgressBar: function() {
      let startTime = Date.parse(new Date(this.startTime));
      let currentTime = Date.parse(new Date());
      let endTime = Date.parse(new Date(this.endTime));
      let interval = parseFloat(
        (currentTime - startTime) / (endTime - startTime) * 100
      ).toFixed(2);
      this.progress = 100-interval;
    }
  },
}
</script>

<style scoped>

</style>
