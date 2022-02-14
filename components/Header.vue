<template>
  <div class="header">
    <div class="mob-menu" v-if="mobMenuIsOpen">
      <div class="mob-nav">
        <div class="mob-nav-wrapper">
          <span class="mob-nav__item" v-for="item in mobileNavList">{{ item }}</span>
        </div>
        <div class="close-button" @click="mobMenuIsOpen = false">close x</div>
      </div>
    </div>
    <div class="header__mobile-wrapper">
      <div class="mobile-nav">
        <div class="hamburger-button" @click="openMobMenu">
          <div class="line"></div>
          <div class="line"></div>
          <div class="line"></div>
        </div>
        <button class="button button__connect">Connect</button>
      </div>
    </div>
    <div class="header__wrapper">
      <div class="nav-container">
        <div class="logo">
          <HeaderSharkSVG/>
        </div>
        <div class="nav">
          <a :href="item.url" class="nav__item" v-for="item in navList">{{ item.label }}</a>
        </div>
        <button class="button button__connect">Connect</button>
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
        { label: 'NFT ART',url: '#'},
        { label: 'Rarity Upgrade',url: '#'},
        { label: 'Club',url: '#'},
        { label: 'Game',url: '#'},
        { label: 'FAQ',url: '#'},
        { label: 'Roadmap',url: '#'},
        { label: 'Team',url: '#'},
        { label: 'Partners',url: '#'},
      ],
      mobMenuIsOpen: false,
      mobileNavList: [
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
  methods:{
    openMobMenu() {
      this.mobMenuIsOpen = !this.mobMenuIsOpen
    }
  },
  components: {HeaderSharkSVG}
}
</script>

<style scoped>

</style>
