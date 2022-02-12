<template>
  <div class="key-facts">
    <div class="intro__container">
      <h3 class="key-facts__title">
        <span class="platforms__title_yellow">KEY FACTS</span> ABOUT SHARKCOIN:
      </h3>
      <div class="key-facts__wrapper">
        <div class="key-facts__item">
          <img :src="require(`assets/img/shark_green.svg`)" class="key-facts__svg"/>
          <div class="key-facts__item-text">
            <h4 class="key-facts__item-description">Developed on:</h4>
            <p class="key-facts__item-name">BSC blockchain</p>
          </div>
        </div>
        <div class="key-facts__item">
          <img :src="require(`assets/img/shark_yellow.svg`)" class="key-facts__svg"/>
          <div class="key-facts__item-text">
            <h4 class="key-facts__item-description">Total supply:</h4>
            <p class="key-facts__item-name">1 billion SHRK</p>
          </div>
          <div class="key-facts__item-text">
            <h4 class="key-facts__item-description">Initial market cap:</h4>
            <p class="key-facts__item-name">$ 308,480</p>
          </div>
        </div>
        <div class="key-facts__item">
          <img :src="require(`assets/img/shark_red.svg`)" class="key-facts__svg"/>
          <div class="key-facts__item-text">
            <h4 class="key-facts__item-description">The basic token price:</h4>
            <p class="key-facts__item-name">0,02 USD</p>
          </div>
        </div>
        <div class="key-facts__item">
          <img :src="require(`assets/img/shark_blue.svg`)" class="key-facts__svg"/>
          <div class="key-facts__item-text">
            <h4 class="key-facts__item-description">IDO date:</h4>
            <p class="key-facts__item-name">3 March 2022</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "KeyFacts",
}
</script>

<style scoped>

</style>
