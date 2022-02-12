<template>
  <div class="platforms">
    <div class="platforms__container intro__container">
      <h3 class="platforms__title">
        <span class="platforms__title_yellow">will be distributed</span> on the platforms:
      </h3>
      <div class="platforms__logos">
        <div class="platforms__item">
          <div>
            <img :src="require(`assets/img/logos/seedify.png`)" alt="">
          </div>
          <div>
            <img :src="require(`assets/img/logos/enjinstarter.png`)" alt="">
          </div>
          <div>
            <img :src="require(`assets/img/logos/oxbull.png`)" alt="">
          </div>
        </div>
        <div class="platforms__item">
          <div>
            <img :src="require(`assets/img/logos/synapse.png`)" alt="">
          </div>
          <div>
            <img :src="require(`assets/img/logos/prostarter.png`)" alt="">
          </div>
          <div>
            <img :src="require(`assets/img/logos/games_pad.png`)" alt="">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Platforms",
  data() {
    return {

    }
  }
}
</script>

<style scoped>

</style>
