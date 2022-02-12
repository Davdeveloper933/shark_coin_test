<template>
  <div class="wrapper">
    <div class="mob-menu" v-if="mobMenuIsOpen">
      <div class="mob-nav">
      <div class="mob-nav-wrapper">
        <span class="mob-nav__item" v-for="item in navList">{{ item }}</span>
      </div>
        <div class="close-button" @click="mobMenuIsOpen = false">close x</div>
      </div>
    </div>
    <Header @open-menu="openMobMenu"/>
    <div class="content">
      <Intro/>
      <Platforms/>
      <KeyFacts/>
    </div>
    <Footer/>
  </div>
</template>

<script>
import Header from "~/components/Header";
import Footer from "~/components/Footer";
import Intro from "~/components/Intro";
import Platforms from "~/components/Platforms";
import KeyFacts from "~/components/KeyFacts";
export default {
  name: 'IndexPage',
  data() {
    return {
      mobMenuIsOpen: false,
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
  methods:{
    openMobMenu() {
      this.mobMenuIsOpen = !this.mobMenuIsOpen
    }
  },
  components: {KeyFacts, Platforms, Intro, Footer, Header}
}
</script>
