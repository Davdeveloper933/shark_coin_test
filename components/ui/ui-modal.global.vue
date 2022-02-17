<template>
  <transition name="modal">
    <div class="modal-bg">
      <div class="modal-wrapper">
        <div class="modal-inner">
          <div class="modal-stage">
            <div class="modal-slide">
              <div class="modal-container">
                <!-- Стандартный popup :: start -->
                <div
                  class="modal-content"
                  :style="{maxWidth}"
                  role="dialog"
                >
                  <button
                    v-if="closeBtn"
                    class="modal-close"
                    @click="closeModal"
                  >
                    <!-- <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                      <path d="M13 12l5-5-1-1-5 5-5-5-1 1 5 5-5 5 1 1 5-5 5 5 1-1z" />
                    </svg> -->

                    <svg width="27" height="27" viewBox="0 0 27 27" fill="none" xmlns="http://www.w3.org/2000/svg">
                      <path d="M26.3287 23.5536L23.5269 26.3553L0.89952 3.72792L3.70126 0.926178L26.3287 23.5536ZM26.3852 3.75778L3.75781 26.3852L0.89952 23.5269L23.5269 0.899495L26.3852 3.75778Z" fill="white"/>
                    </svg>
                  </button>

                  <div class="modal-body">
                    <div class="modal-header-icon m-b-50">
<!--                      <img v-if="icon === 'error'" :src="require('~/assets/img/icon-error.svg')" alt="">-->
<!--                      <img v-else :src="require('~/assets/img/icon-success.svg')" alt="">-->
                    </div>

                    <h2 class="modal-title text-uppercase text-center m-b-50">
                      <slot name="title" />
                    </h2>

                    <slot />
                  </div>
                </div>
                <!-- Стандартный popup :: end -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "UiModal",
  props: {
    // Show close button
    closeBtn: {
      type: Boolean,
      default: false
    },
    maxWidth: {
      type: String,
      default: "580px"
    },
    icon: {
      type: String,
      default: "success"
    }
  },
  mounted () {
    document.querySelector("body").classList.add("modal-open");
    window.addEventListener("keydown", this.escCloseModal);
  },
  beforeDestroy () {
    document.querySelector("body").classList.remove("modal-open");
    window.removeEventListener("keydown", this.escCloseModal);
  },
  methods: {
    escCloseModal (e) {
      if (this.closeBtn && e.key === "Escape") {
        this.closeModal();
      }
    },
    closeModal () {
      this.$emit("close");
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@/assets/style/mixins/mixins";
@import "~@/assets/style/variables";

$modal-overlay-bg: #0C0D22;
$modal-bg: linear-gradient(124.1deg, #FFFFFF 51.07%, rgba(255, 255, 255, 0) 176.63%);
$padding-top: 0; // зависит от высоты header
.modal-bg {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 999;
  position: fixed;
  outline: none !important;
  //-webkit-backface-visibility: hidden;
  background-color: rgba($modal-overlay-bg, 0.9);
  //backdrop-filter: blur(30px);
  transition: opacity 0.3s ease;
}

.modal-iframe {
  .modal-content {
    background: $modal-bg;
    padding: 20px;
  }
}

.modal-content {
  width: 100%;
  position: relative;
  margin: auto;
  padding: 30px;
  background: $modal-bg;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 0;
  transition: all 0.3s ease;
  &:before {
    content: "";
    position: absolute;
    top: -11px;
    left: -11px;
    width: 100%;
    height: 92%;
    max-height: 615px;
    z-index: -1;
    background: linear-gradient(110.52deg, #5758C1 -1.87%, #FE0FC4 25.68%);

    @include respond-before("md") {
      top: -16px;
      left: -16px;
    }
    @include respond-before("lg") {
      top: -30px;
      left: -30px;
    }
  }
  &:after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: -1;
    background: linear-gradient(124.1deg, #FFFFFF 51.07%, rgba(255, 255, 255, 0) 176.63%);
    box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
  }
}

.modal-wrapper {
  -webkit-backface-visibility: hidden;
  height: 100%;
  left: 0;
  outline: 0;
  position: fixed;
  -webkit-tap-highlight-color: transparent;
  top: 0;
  -ms-touch-action: manipulation;
  touch-action: manipulation;
  -webkit-transform: translateZ(0);
  transform: translateZ(0);
  width: 100%;
  z-index: 99992;
}

.modal-inner,
.modal-stage {
  bottom: 0;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
}

.modal-stage {
  direction: ltr;
  -webkit-transform: translateZ(0);
  transform: translateZ(0);
  z-index: 99994;
  overflow: hidden;
}

.modal-slide {
  -webkit-backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
  left: 0;
  outline: 0;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
  padding: $padding-top 15px 0;
  position: absolute;
  text-align: center;
  top: 0;
  -webkit-transition-property: opacity, -webkit-transform;
  transition-property: opacity, -webkit-transform;
  -o-transition-property: transform, opacity;
  transition-property: transform, opacity;
  transition-property: transform, opacity, -webkit-transform;
  white-space: normal;
  width: 100%;
  z-index: 99994;
}

.modal-container {
  display: inline-block;
  margin: 0;
  max-width: 100%;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
  padding: 20px 0;
  position: relative;
  text-align: left;
  vertical-align: middle;
}

.modal-close {
  background: none;
  border: 0;
  display: inline-block;
  height: 20px;
  width: 20px;
  padding: 0;
  right: -53px;
  top: 0;
  margin: 0;
  transition: color .2s;
  vertical-align: top;
  visibility: inherit;
  border-radius: 0;
  color: currentColor;
  cursor: pointer;
  opacity: 1;
  position: absolute;
  z-index: 401;

  //@include respond-before("md") {
  //  left: 30px;
  //  top: 30px;
  //}

  svg {
    display: block;
    height: 100%;
    overflow: visible;
    position: relative;
    width: 100%;

    //path {
    //  fill: currentColor;
    //}
  }
}

.modal-header {
  //@include modal-header;
}

.modal-body {
  padding: 0;
  font-size: 16px;
}

.modal-footer {
  margin-top: 30px;

  &__action {
    text-align: center;
  }

  &__top {
    margin-bottom: 20px;
  }

  &__bottom {
    margin-top: 20px;
  }
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-wrapper,
.modal-leave-active .modal-wrapper {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
