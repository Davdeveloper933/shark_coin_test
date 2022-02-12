<template>
  <div class="intro">
    <div class="intro__container">
      <h2 class="intro__title">Sharkcoin</h2>
      <div class="sharkcoin-ido">
        <CoinSVG class="sharkcoin-ido__coin"/>
        <div class="sharkcoin-ido__wrapper">
        <h3 class="sharkcoin-ido__title">Sharkcoin (SHRK) IDO</h3>
        <div class="day-counter">
          <div class="day-counter__item">
            <div class="day-counter__num">34</div>
            <div class="day-counter__text">Days</div>
          </div>
          <div class="day-counter__item">
            <div class="day-counter__num">09</div>
            <div class="day-counter__text">Hours</div>
          </div>
          <div class="day-counter__item">
            <div class="day-counter__num">21</div>
            <div class="day-counter__text">Minutes</div>
          </div>
          <div class="day-counter__item">
            <div class="day-counter__num">42</div>
            <div class="day-counter__text">Seconds</div>
          </div>
        </div>
          <div class="join">
            <h3 class="join__title">You can join and buy Sharkcoins  by using:</h3>
            <div class="join__buttons">
              <div class="button button__metamask">
                <img :src="require('assets/img/fox.png')" class="button__metamask-img" alt="">
                Metamask
              </div>
              <div class="button button__connect">wallet connect</div>
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
}
</script>

<style scoped>

</style>
