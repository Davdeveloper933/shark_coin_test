<template>
  <div class="header">
    <div class="header__mobile-wrapper">
      <div class="mobile-nav">
        <div class="hamburger-button" @click="$emit('open-menu')">
          <div class="line"></div>
          <div class="line"></div>
          <div class="line"></div>
        </div>
        <div class="button button__connect">Connect</div>
      </div>
    </div>
    <div class="header__wrapper">
      <div class="nav-container">
        <div class="logo">
          <HeaderSharkSVG/>
        </div>
        <div class="nav">
          <span class="nav__item" v-for="item in navList">{{ item }}</span>
        </div>
        <div class="button button__connect">Connect</div>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderSharkSVG from "~/components/SVG/HeaderSharkSVG";
export default {
  name: "Header",
  data() {
    return {
      navList: [
        'NFT ART',
        'Rarity Upgrade',
        'Club',
        'Game',
        'FAQ',
        'Roadmap',
        'Team',
        'Partners'
      ]
    }
  },
  components: {HeaderSharkSVG}
}
</script>

<style scoped>

</style>
