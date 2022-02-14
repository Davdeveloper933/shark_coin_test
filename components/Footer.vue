<template>
  <div class="footer">
    <div class="footer__wrapper">
      <div class="footer__icons">
        <a
          class="footer__icons-item"
          v-for="item in footerIconLinks"
          :href="item.url"
        >
          <span class="mdi" :class="item.icon"></span>
          <p class="footer__icons-item__text">{{ item.label }}</p>
        </a>
      </div>
      <div class="footer__nav">
        <a
          :href="item.url"
          class="footer__nav-link"
          v-for="item in footerNav"
        >
          {{ item.label }}
        </a>
      </div>
      <div class="copyright">
        <p class="copyright__text">
          SharkRace Club produced by TizerWallet OU registered in Estonia (No. 14648578)
          Tallin, Lasnamae Linnaosa, Vaike-Paala tn 2, 11415
        </p>
        <p class="copyright__text">(c) 2022 SharkPlace Club. All Rights Reserved</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      footerNav:[
        { label: 'Support',url: '#'},
        { label: 'Terms & conditions',url: '#'},
        { label: 'WhitePaper',url: '#'},
      ],
      footerIconLinks: [
        { label: '@sharkraceclub', url:'#',icon:'mdi-twitter'},
        { label: '@sharkraceclub', url:'#',icon:'mdi-instagram'},
        { label: '@sharkraceclub', url:'#',icon:'mdi-youtube'},
        { label: '@sharkraceclub', url:'#',icon:'mdi-facebook'},
        { label: '@sharkraceclub', url:'#',icon:'mdi-linkedin'},
      ]
    }
  }
}
</script>

<style scoped>

</style>
