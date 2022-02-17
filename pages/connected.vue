<template>
  <div class="intro__container">
    <h2 class="intro__title">Sharkcoin</h2>
    <div class="buy-tokens">
      <div class="buy-tokens__wrapper">
        <div class="buy-tokens__overlay"
             v-if="clickedOnBuyToken"
             v-click-outside="closeOverLay"
        >
          <div class="buy-tokens__overlay__content">
          <span class="buy-tokens__overlay__text">
            You can join and buy Sharkcoins  by using:
          </span>
            <div class="buy-tokens__overlay__buttons">
              <button class="button button__metamask"
                      @click="openModal"
              >
                <img :src="require('assets/img/fox.svg')" class="button__metamask-img" alt="">
                Metamask
              </button>
              <button class="button button__connect">wallet connect</button>
            </div>
          </div>
        </div>
        <div class="buy-tokens__select">
          <div class="erc20">
            ERC20
          </div>
          <div class="mp-form__item">
            <div class="mp-form__label buy-tokens__label">
              <span class="buy-tokens__label-text">You send</span>
              <span class="buy-tokens__label-text">Tether (ERC20)</span>
            </div>
            <div class="mp-form__field">
              <ui-text-field
                v-model.number="sendInput"
                inputmode="decimal"
                type="number"
                min="0"
                step="0.01"
              >
                <template #append>
                  <ui-select
                    v-model="sendCoin"
                    :options="sendCoinList"
                  >
                    <template #default="{ option }">
                      <img
                        v-if="option.symbol"
                        :src="require(`~/assets/img/tokens/${option.symbol}.svg`)"
                        alt=""
                      >
                      {{ option.symbol.toUpperCase() }}
                    </template>
                  </ui-select>
                </template>
              </ui-text-field>
            </div>
          </div>
        </div>
        <div class="all-fees-included">
          <div class="all-fees-included__text">
            1 USDT20 ≈ 0.00030922 ETH &bull;
            All fees <span class="yellow-text">included</span>
          </div>
        </div>
        <div class="buy-tokens__select">
          <div class="mp-form__item">
            <div class="mp-form__label buy-tokens__label">
              <span class="buy-tokens__label-text">You get</span>
              <span class="buy-tokens__label-text">SharkCoin</span>
            </div>
            <div class="mp-form__field">
              <ui-text-field
                v-model.number="sendInput"
                inputmode="decimal"
                type="number"
                min="0"
                step="0.01"
              >
                <template #append>
                  <ui-select
                    v-model="sendCoin"
                    :options="sendCoinList"
                  >
                    <template #default="{ option }">
                      <img
                        v-if="option.symbol"
                        :src="require(`~/assets/img/tokens/${option.symbol}.svg`)"
                        alt=""
                      >
                      {{ option.symbol.toUpperCase() }}
                    </template>
                  </ui-select>
                </template>
              </ui-text-field>
            </div>
          </div>
        </div>
        <div class="buy-tokens__button">
          <button class="button button__connect" @click="closeOverLay">Buy tokens</button>
        </div>
      </div>
    </div>
    <div class="binance">
      <div class="binance__wrapper">
        <p class="binance__text">
          The project is made on the
        </p>
        <div class="binance__logo">
          <img :src="require(`assets/img/logos/binance.svg`)" alt="">
        </div>
      </div>
    </div>
    <KeyFacts/>
    <ui-modal
      v-if="showModal"
      :icon="modal"
      :close-btn="!modalHideClose"
      max-width="458px"
      @close="closeModal"
    >
<!--      первый вариант модалки-->
        <div class="metamask-modal">
          <div class="metamask-modal__img metamask-modal__img-metamask">
            <img :src="require(`assets/img/fox.svg`)" alt="">
          </div>
          <h3 class="oops">Oops, sorry...</h3>
          <p class="metamask-modal__text">
            The current browser does not support Metamask. If you want to use it, use the following browsers: Google Chrome, Internet Explorer
          </p>
          <div class="metamask-modal__button">
            <button class="button button__connect" @click="closeOverLay">Use wallet connect</button>
          </div>
        </div>

<!--      второй вариант модалки-->
<!--      <div class="metamask-modal something-wrong-modal">-->
<!--        <div class="metamask-modal__img metamask-modal__img-error">-->
<!--          <img :src="require(`assets/img/icon-error.svg`)" alt="">-->
<!--        </div>-->
<!--        <h3 class="oops">Something went wrong</h3>-->
<!--        <p class="metamask-modal__text">-->
<!--          You were not succeed to buy items, check up your internet connection / available balance / connection with your wallet and try again-->
<!--        </p>-->
<!--        <div class="metamask-modal__button">-->
<!--          <button class="button button__connect" @click="closeOverLay">Try Again</button>-->
<!--        </div>-->
<!--      </div>-->

<!--      третий вариант модалки-->
<!--      <div class="metamask-modal something-wrong-modal">-->
<!--        <div class="metamask-modal__img metamask-modal__img-error">-->
<!--          <img :src="require(`assets/img/icon-success.svg`)" alt="">-->
<!--        </div>-->
<!--        <h3 class="oops">You’ve successfully purchased items-->
<!--        </h3>-->
<!--        <p class="metamask-modal__text">-->
<!--          AYou can watch your accessories in a dressing room. There you can try them on every NFT Shark you’ve got and merge them creating completely new NFT-->
<!--        </p>-->
<!--        <div class="follow-on-soc-networks">-->
<!--          <h3 class="follow-on-soc-networks__title">Follow us on social networks:</h3>-->
<!--          <div class="follow-us-on-soc-networks__links">-->

<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="desc">-->
<!--        <ul v-if="errors.length" class="list list&#45;&#45;none">-->
<!--          <li v-for="(error, idx) in errors" :key="idx" class="">-->
<!--            {{ error }}-->
<!--          </li>-->
<!--        </ul>-->
<!--      </div>-->
<!--      <div class="text-center m-l-a m-r-a m-t-80" style="max-width: 700px;">-->
<!--        <template v-if="modalHideClose">-->
<!--          <div>-->
<!--            <ui-preloader />-->
<!--          </div>-->
<!--          <button-->
<!--            v-if="wallet && wallet.type !== 'walletconnect'"-->
<!--            class="btn btn-solid btn-solid&#45;&#45;secondary btn-wide m-t-30"-->
<!--            @click="switchBinanceNetwork"-->
<!--            v-text="'Switch network'"-->
<!--          />-->
<!--        </template>-->
<!--        <button-->
<!--          v-else-->
<!--          class="btn btn-solid btn-solid&#45;&#45;secondary btn-wide btn-big"-->
<!--          @click="closeModal"-->
<!--          v-text="modalLabels.closeBtn"-->
<!--        />-->
<!--      </div>-->
    </ui-modal>
  </div>
</template>

<script>
import UiTextField from "~/components/ui/ui-text-field.global";
import UiSelect from "~/components/ui/ui-select.global";
import KeyFacts from "~/components/KeyFacts";
import UiModal from "~/components/ui/ui-modal.global";
export default {
  name: "connected",
  components: {UiModal, KeyFacts, UiSelect, UiTextField},
  data () {
    return {
      showModal: false,
      modalHideClose: false,
      modalLabels: {
        title: "",
        closeBtn: "Ok"
      },
      modal: null,
      errors: [],
      clickedOnBuyToken:false,
      sendInput: 0,
      sendCoinList: [
        {symbol:"usdt",amount:2000},
        {symbol:"bnb",amount:0.78}
      ],
      sendCoin: {
        symbol: ""
      },
      theLinksOfSocialNetworks: [
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
        { icon: '', url: '#'},
      ]
    }
  },
  methods:{
    optionSymbol (symbol, lowercase = false) {
      if (!symbol) {
        return;
      }
      const output = symbol.split("USDT")[0];
      if (lowercase) {
        return output.toLowerCase();
      }
      return output;
    },
    /** Слушатель события ввода отдаваемых монет */
    onSendInput () {
      // this.sendInputUsd = this.$toUsd(this.sendCoin.symbol, this.sendInput);
      // this.getInput = this.sendInputUsd / this.price; // this.$fromUsd(this.$symbolCurrencySplitUsdt(this.getCoin.symbol), this.sendInputUsd);
      //
      // this.validateForm();
    },
    closeOverLay () {
      this.clickedOnBuyToken = !this.clickedOnBuyToken
    },
    /** Открыть модальное окно */
    openModal (modal, hideClose, labels) {
      this.showModal = true;
      this.modal = modal;
      this.modalHideClose = hideClose;
      if (labels) {
        this.modalLabels = labels;
      }
    },
    /** Закрыть модальное окно */
    closeModal () {
      this.showModal = false;
      this.modal = "";
      this.modalHideClose = false;
      this.errors = [];
      this.modalLabels = {
        title: "",
        closeBtn: "Ok, close"
      };
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/style/mixins/mixins";

.buy-tokens {
  max-width: 384px;
  &__select {
    position: relative;
  }
  &__container {
    max-width: 384px;
    margin: 0 auto;
  }
  &__wrapper {
    background: linear-gradient(180deg, #0C0D22 0%, rgba(12, 13, 34, 0.8) 68.37%, rgba(12, 13, 34, 0) 100%);
    border-radius: 26px;
    padding: 24px 20px 60px 20px;
  }
  &__button {
    margin-top: 40px;
    display: flex;
    justify-content: center;
  }
  &__label {
    display: flex;
    justify-content: space-between;
    &-text {
      font-size: 14px;
      line-height: 18px;
      letter-spacing: -0.04em;
      color: #858799;
    }
  }
}

/* Форма минтпасса */
.color-gray-light {
  color: #bebfbc;
}

/** Форма MintPass*/
.mp {
  max-width: 800px;
  margin: auto;
  padding: 0 15px;

  &-header {
    position: relative;
    background: radial-gradient(110.09% 191.87% at 34.84% -25.88%, #323634 0%, rgba(17, 20, 19, 0.8) 100%);
    border-radius: 30px 30px 0 0;
    z-index: 10;

    &__center {
      justify-content: center;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      height: 70px;
    }

    &__left,
    &__right {
      display: none;

      @include respond-before("md") {
        display: block;
        position: absolute;
        bottom: -80px;
      }
    }

    &__left {
      left: -15px;

      @include respond-before("lg") {
        left: -27px;
      }
    }

    &__right {
      right: -15px;

      @include respond-before("lg") {
        right: -35px;
      }
    }
  }

  &-body {
    position: relative;
    background: radial-gradient(110.09% 191.87% at 34.84% -25.88%, #1e1e1e 0%, rgba(17, 20, 19, 0.95) 100%);
    border-radius: 0 0 30px 30px;
    padding: 20px 20px 30px;
    z-index: 20;

    @include respond-before("sm") {
      padding: 20px 30px 40px;
    }

    @include respond-before("md") {
      display: flex;
      flex-wrap: wrap;
      padding: 30px 40px 50px;
    }

    &__left,
    &__right {
      @include respond-before("md") {
        width: 50%;
      }
    }

    &__left {
      @include respond-before("md") {
        padding-right: 25px;
        order: 1;
      }
    }

    &__right {
      margin-bottom: 30px;

      @include respond-before("md") {
        order: 2;
        margin-bottom: 0;
      }
    }

    &__footer {
      flex: 1;
      margin-top: 40px;

      @include respond-before("md") {
        order: 3;
      }
    }
  }

  &-info {
    display: flex;
    align-items: center;
    @include fontTTHoves("medium");
    font-size: 28px;

    img {
      width: 40px;
      margin-right: 15px;
    }
  }

  &-desc {
    font-size: 12px;
    color: rgba(#6C766F, .7);
  }

  &-select {
    background: transparent url("data:image/svg+xml,%3Csvg width='24' height='24' viewBox='0 0 24 24' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M16.9999 9.17C16.8126 8.98375 16.5591 8.87921 16.2949 8.87921C16.0308 8.87921 15.7773 8.98375 15.5899 9.17L11.9999 12.71L8.45995 9.17C8.27259 8.98375 8.01913 8.87921 7.75495 8.87921C7.49076 8.87921 7.23731 8.98375 7.04995 9.17C6.95622 9.26297 6.88183 9.37357 6.83106 9.49543C6.78029 9.61729 6.75415 9.74799 6.75415 9.88C6.75415 10.012 6.78029 10.1427 6.83106 10.2646C6.88183 10.3864 6.95622 10.497 7.04995 10.59L11.2899 14.83C11.3829 14.9237 11.4935 14.9981 11.6154 15.0489C11.7372 15.0997 11.8679 15.1258 11.9999 15.1258C12.132 15.1258 12.2627 15.0997 12.3845 15.0489C12.5064 14.9981 12.617 14.9237 12.7099 14.83L16.9999 10.59C17.0937 10.497 17.1681 10.3864 17.2188 10.2646C17.2696 10.1427 17.2957 10.012 17.2957 9.88C17.2957 9.74799 17.2696 9.61729 17.2188 9.49543C17.1681 9.37357 17.0937 9.26297 16.9999 9.17Z' fill='%23FDFF87'/%3E%3C/svg%3E%0A") no-repeat 100% 50%;
    padding-right: 30px;
    border: 0;
    text-align: center;
    color: #fdff87;
    @include fontTTHoves("medium");
    font-size: 20px;
    text-transform: capitalize;
    @include appearance(none);

    @include respond-before("lg") {
      font-size: 24px;
    }
  }

  /* Форма минтпасса */
  &-form {
    &__item {
      background: #121312;
      border-radius: 8px;
      padding: 16px;
    }

    &__item + &__item {
      margin-top: 10px;
    }

    &__label {
      @include fontTTHoves("medium");
      color: #6c766f;
      margin-bottom: 10px;
    }

    &__bottom {
      margin-top: 15px;
    }

    &__card-get {
      display: flex;
      align-items: center;
      @include fontTTHoves("medium");
      text-transform: capitalize;
      background: #212321;
      border: 1px solid #121312;
      border-radius: 20px;
      padding: 8px 12px 8px 12px;
      min-width: 116px;
      margin-left: -15px; // same ui-select component
      margin-right: -19px; // same ui-select component

      img {
        width: 16px;
        margin-right: 8px;
      }
    }

    &::v-deep {
      .ui-input-text {
        background: transparent;
        padding-left: 0;

        &__input {
          padding-top: 0;
          padding-left: 0;
          padding-bottom: 0;

          input {
            @include fontTTHoves("bold");
            font-size: 28px;
          }
        }

      }

      .ui-select {
        @include fontTTHoves("medium");
        text-transform: uppercase;

        &__container {
          background: #212321;
          border: 1px solid #121312;
          border-radius: 20px;
        }

        &__selected {
          padding-right: 40px;
          min-height: 1px;
          width: 116px;

          &--single {
            padding-right: 12px;
          }
        }

        &__selected,
        &__item {
          padding: 8px;
          display: flex;
          align-items: center;

          img {
            width: 24px;
            height: 24px;
            margin-right: 8px;
          }
        }

        &__list {
          background: #212321;
          border-radius: 20px;
        }

        &__item:hover {
          background: lighten(#212321, 5%);
        }
      }
    }
  }

  /* Слайдер */
  &-slider {
    max-width: 850px;
    width: 100%;
    padding: 0 15px;
    margin: 0 auto 110px;

    &-nav {
      position: absolute;
      background: linear-gradient(180deg, #91ff87 0%, #44b550 100%);
      box-shadow: 0 4px 0 #35833b;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      top: 50%;
      text-align: center;
      margin-top: -20px;

      svg {
        width: 16px;
      }

      &:not([disabled]):hover {
        color: #fff;
        background: linear-gradient(180deg, #44b550 0%, #44b550 100%);
      }

      &__prev {
        left: 0;
      }

      &__next {
        right: 0;
      }
    }

    &__content {
      @include respond-before("md") {
        display: flex;
        align-items: center;
      }
    }

    &__fig {
      margin-bottom: 15px;
      padding: 0 50px;
      position: relative;
      text-align: center;

      @include respond-before("md") {
        width: 300px;
        margin: 0;
      }

      img {
        @include respond-before("sm") {
          @include respond-to("md") {
            max-width: 280px;
          }
        }
      }
    }

    &__cnt {
      padding-left: 30px;

      @include respond-before("md") {
        flex: 1;
      }
    }

    &__title {
      color: var(--color-secondary);
      margin-bottom: 20px;
      @include fontTTHoves("medium");
      font-size: 24px;
      text-transform: capitalize;
    }

    &__desc {
      font-size: 16px;
    }

    &::v-deep {
      .swiper-container {
        padding-bottom: 30px;
      }

      .swiper-pagination-bullets {
        bottom: 0;
      }

      .swiper-pagination-bullet {
        background: var(--color-secondary);
      }
    }
  }
}

/** Кошелек пользователя в форме MintPass*/
.user-wallet {
  &__title {
    font-size: 14px;
  }

  &__value {
    @include fontTTHoves("medium");
    text-transform: uppercase;

    span {
      color: rgba(#fff, .7);
    }
  }
}

.btn-wide {
  font-size: 20px;
  padding-left: 60px;
  padding-right: 60px;
}

.cover {
  padding-bottom: 80px;
  overflow: hidden;

  /* Плавающие карточки возле формы MintPass */
  &-float {
    z-index: 3;
    height: 150px;
    margin-top: 30px;

    @include respond-before("xs") {
      height: 230px;
    }
    @include respond-before("md") {
      height: 360px;
    }
    @include respond-before("lg") {
      bottom: 50%;
      margin-top: 0;
      height: auto;
      position: absolute;
      left: 0;
      right: 0;
    }

    &__left,
    &__right {
      position: absolute;
      width: 142px;
      height: 215px;

      @include respond-before("sm") {
        width: 201px;
        height: 305px;
      }
      @include respond-before("md") {
        width: 286px;
        height: 431px;
      }
    }

    &__left {
      left: -20px;
      transform: rotate(5deg);

      @include respond-before("lg") { // 992
        left: auto;
        right: calc(90% - 0px);
      }
      @include respond-before("xl") { // 1200
        right: calc(90% - 30px);
      }
    }

    &__right {
      right: -20px;
      transform: rotate(-5deg);

      @include respond-before("lg") { // 992
        right: 0;
        left: calc(90% - 0px);
      }
      @include respond-before("xl") { // 1200
        left: calc(90% - 30px);
      }
    }
  }

}

.banner {
  padding-top: 110px;

  &:after {
    top: -20%;
  }

  &__title,
  &__text {
    text-align: center;
  }

  &__title {

    @include respond-to("sm") {
      span {
        display: block;
      }
    }
    @include respond-before("md") {
      font-size: 40px;
    }
  }

  &__text {
    max-width: 250px;
    margin-left: auto;
    margin-right: auto;
  }
}

//.content {
//  background: url("~/assets/img/bg-tree.svg") no-repeat 70% 50%;
//  background-size: 1000px auto;
//  position: relative;
//  z-index: 0;
//  padding-top: 200px;
//
//  @include respond-before("md") {
//    padding-top: 150px;
//  }
//  @include respond-before("lg") {
//    padding-top: 0;
//    background-position: 50% 0;
//    background-size: contain;
//  }
//
//  &-bg {
//    position: absolute;
//    z-index: -1;
//
//    &--top {
//      &-left,
//      &-right {
//        top: -140px;
//
//        @include respond-to("pre-md") {
//          width: 300px;
//        }
//      }
//
//      &-left {
//        left: 0;
//      }
//
//      &-right {
//        right: 0;
//
//        @include respond-to("pre-md") {
//          transform: scale(1, -1);
//        }
//      }
//    }
//
//    &--bottom {
//      &-left {
//        left: 0;
//        bottom: 200px;
//
//        @include respond-before("xxs") {
//          bottom: 90px;
//        }
//        @include respond-before("md") {
//          bottom: 125px;
//        }
//        @include respond-before("lg") {
//          bottom: 0;
//        }
//      }
//
//      &-right {
//        right: 0;
//        bottom: 200px;
//
//        @include respond-before("xxs") {
//          bottom: 90px;
//        }
//        @include respond-before("md") {
//          bottom: 0;
//        }
//      }
//    }
//  }
//}

/** Зеленый фон в середине страницы */
//.big-blur {
//  background: url("~/assets/img/big-blur.svg") no-repeat 50% 0%;
//  background-size: cover;
//  padding-top: 200px;
//
//  @include respond-before("md") {
//    background-size: 100% auto;
//  }
//}

.partners {
  &__container {
    max-width: 850px;
    padding: 0 15px;
    width: 100%;
    margin: 0 auto;
  }

  &__item {
    margin-bottom: 40px;
    text-align: center;
    display: block;
    width: 100%;

    @include respond-before("sm") {
      @include respond-to("md") {
        width: calc(50% - 20px);
        margin: 0 10px 60px;

        &:nth-last-child(-n+2) {
          margin-bottom: 0;
        }
      }
    }

    @include respond-before("md") {
      width: calc(33.3333% - 20px);
      margin: 0 10px 60px;

      &:nth-last-child(-n+3) {
        margin-bottom: 0;
      }
    }

    img {
      height: 110px;
    }
  }

  .container {
    @include respond-before("sm") {
      flex-wrap: wrap;
      display: flex;
      margin: auto;
      //margin-left: -10px;
      //margin-right: -10px;
    }
  }
}

.facts {
  margin-bottom: 100px;

  &__container {
    max-width: 850px;
    padding: 0 15px;
    width: 100%;
    margin: 0 auto;
  }

  &__title {
    text-align: center;
    @include fontTTHoves("medium");
    font-size: 24px;
    margin-bottom: 40px;
  }

  &__row {
    display: flex;
    flex-wrap: wrap;
    margin-left: -10px;
    margin-right: -10px;
  }

  &__item {
    width: 50%;
    padding-left: 10px;
    padding-right: 10px;

    @include respond-before("md") {
      width: 25%;
    }
  }

  .fact-item {
    text-align: center;

    &__img {
      margin-bottom: 15px;
    }

    &__label {
      color: rgba(#fff, .7);
      font-size: 14px;
      margin-bottom: 5px;
    }

    &__txt {
      @include fontTTHoves("medium");
      font-size: 18px;
      margin-bottom: 20px;
    }
  }
}

.feature {
  margin-bottom: 0;
  padding-bottom: 320px;

  @include respond-before("md") {
    padding-bottom: 50px;
  }

  &__container {
    max-width: 1040px;
    padding: 0 15px;
    width: 100%;
    margin: 0 auto;
  }

  .container {
    @include respond-before("md") {
      flex-wrap: wrap;
      display: flex;
      margin-left: -10px;
      margin-right: -10px;
    }
  }

  &__col {
    padding-left: 10px;
    padding-right: 10px;
    margin-bottom: 20px;

    @include respond-before("md") {
      width: 50%;
    }
    @include respond-before("lg") {
      width: 25%;
    }
  }

  &__item {
    position: relative;
    padding: 40px 20px;
    height: 100%;
    text-align: center;
    margin: auto;
    max-width: 300px;

    @include respond-before("md") {
      max-width: 100%;
    }

    &:before {
      content: "";
      background: radial-gradient(110.09% 191.87% at 34.84% -25.88%, rgba(131, 196, 156, 0) 0%, rgba(39, 152, 90, 0.8) 100%);
      opacity: 0.4;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 0;
    }

    > * {
      position: relative;
      z-index: 1;
    }
  }

  &__img {
    margin-bottom: 20px;
  }

  &__title {
    font-size: 24px;
    line-height: 1.25em;
    letter-spacing: -0.04em;
    margin-bottom: 10px;
  }

  &__txt {
    color: #bebfbc;
  }
}

.bottom-text {
  position: relative;
  margin-top: 400px;

  @include respond-before("md") {
    margin-top: 0;
  }

  //&__blur {
  //  position: absolute;
  //  background: url("~/assets/img/bottom-text-blur.svg") no-repeat 50% 0;
  //  background-size: contain;
  //  left: 0;
  //  right: 0;
  //  top: -40vw;
  //  width: 100%;
  //  margin: auto;
  //  max-width: 1440px;
  //  padding-bottom: 50%;
  //}

  &__container {
    max-width: 1040px;
    padding: 0 15px;
    width: 100%;
    margin: 0 auto;
  }

  &__title {
    font-weight: bold;
    font-size: 26px;
    line-height: 1.35em;
    text-align: center;
    letter-spacing: -0.04em;
    color: #fff;
    max-width: 600px;
    margin: 0 auto 50px;
    padding: 0 15px;

    span, a {
      color: #fdff87;
    }

    @include respond-before("pre-md") {
      font-size: 28px;
    }
    @include respond-before("md") {
      font-size: 40px;
    }
  }

  &__btn {
    text-align: center;

    &__item {
      max-height: 68px;
      margin: 0 auto 80px;
      padding: 20px 60px;
      font-size: 20px;
    }
  }
}

.footer {
  padding-top: 0 !important;
  background: transparent;
}

.site-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  padding: 10px 0;
  z-index: 999;
  transition: padding $transition, background $transition;

  &--fixed {
    background: rgba(#2f4638, .8);
    backdrop-filter: blur(5px);
    box-shadow: 0 4px 10px rgba(#2f4638, .8);
  }

  &-item {
    height: 100%;
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
  }

  &-logo {
    margin-right: 20px;
    margin-left: 0;
    position: relative;
    z-index: 25;

    @include respond-before("lg") {
      margin-right: 20px;
      margin-left: 0;
    }
    @include respond-before("xl") {
      margin-right: 30px;
    }

    img {
      position: relative;
      margin-top: -10px;
    }

    svg {
      @include respond-to("xs") {
        width: 150px;
      }
    }
  }

  &-right {
    display: flex;
    align-items: center;
    flex-flow: row wrap;

    @include respond-before("md") {
      @include respond-to("lg") {
        margin-left: auto;
      }
    }
  }

  &-btn {
    @include respond-to("pre-md") {
      padding-left: 30px;
      padding-right: 30px;
    }
    @include respond-to("xs") {
      padding: 6px 20px;
      font-size: 16px;
    }
  }

  &-space {
    margin-left: auto;
    margin-right: auto;
  }

  &-userbar-mobile {
    @include respond-before("md") {
      display: none;
    }
  }

  &-menu {
    $self: &;
    @include respond-to("lg") {
      display: none;
    }

    &__list {
      list-style-type: none;

      @include respond-before("lg") {
        display: flex;
        flex-wrap: wrap;
        align-items: flex-start;
      }

      @include respond-to("lg") {
        text-align: center;
      }
    }

    &__item {
      margin: 15px auto;
      padding: 0;
      line-height: 1em;
      font-weight: 500;

      @include respond-before("lg") {
        margin: 0;

        &:last-child {
          margin-right: 0;
        }
      }
      @include respond-before("xl") {

      }
    }

    &__link {
      color: #fff;
      display: block;
      padding: 15px 20px; // 15px 26px
      border-radius: 12px;

      @include respond-before("lg") {
        padding: 15px;
      }
      @include respond-before("xl") {
        padding: 15px 20px;
      }

      &:hover {
        color: #91ff87;
      }

      &.nuxt-link-exact-active {
        color: #fdff87;
        font-weight: 600;
      }
    }

    &__top {
      text-align: center;
      margin-bottom: 50px;
    }

    &__bottom {
      margin-top: 50px;
      text-align: center;
    }

    &--mobile {
      position: absolute;
      top: 0;
      right: 0;
      left: 0;
      z-index: 20;
      height: 100vh;
      padding: 70px 15px 40px;
      overflow-y: auto;
      background: var(--body-bg);

      @include respond-before("lg") {
        display: none;
      }

      &-visible {
        display: block;
      }
    }

    &--desktop {
      margin-left: auto;
      margin-right: auto;

      @include respond-to("lg") {
        display: none;
      }
    }
  }

  .btn-burger {
    border-radius: 10px;
    width: 40px;
    height: 40px;
    padding: 0;
    background: rgba(167, 169, 183, 0.07);
    border: 1px solid #cef2ee;
    position: relative;
    z-index: 30;
    margin-left: 30px;

    @include respond-before("lg") {
      display: none;
    }
  }

  .container {
    display: flex;
    align-items: center;
    min-height: 70px;
    margin: auto;
    padding-left: 15px;
    padding-right: 15px;

    @include respond-before("lg") {
      min-height: 70px;
    }
  }
}


</style>
