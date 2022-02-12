<template>
  <div class="footer">
    <div class="footer__wrapper">
      <div class="footer__icons">
        <div class="footer__icons-item">
          <span class="mdi mdi-twitter"></span>
          <p class="footer__icons-item__text">@sharkraceclub</p>
        </div>
        <div class="footer__icons-item">
          <span class="mdi mdi-instagram"></span>
          <p class="footer__icons-item__text">@sharkraceclub</p>
        </div>
        <div class="footer__icons-item">
          <span class="mdi mdi-youtube"></span>
          <p class="footer__icons-item__text">@sharkraceclub</p>
        </div>
        <div class="footer__icons-item">
          <span class="mdi mdi-facebook"></span>
          <p class="footer__icons-item__text">@sharkraceclub</p>
        </div>
        <div class="footer__icons-item">
          <span class="mdi mdi-linkedin"></span>
          <p class="footer__icons-item__text">@sharkraceclub</p>
        </div>
      </div>
      <div class="footer__nav">
        <div
          class="footer__nav-link"
          v-for="link in links"
        >
          {{ link }}
        </div>
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
      links:[
        'Support',
        'Terms & conditions',
        'WhitePaper'
      ]
    }
  }
}
</script>

<style scoped>

</style>
