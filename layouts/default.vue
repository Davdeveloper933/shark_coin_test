<template>
  <div class="wrapper">
    <Header/>
    <div class="content">
      <Nuxt ref="nuxt" />
    </div>
    <Footer/>
  </div>
</template>

<script>
import Header from "~/components/Header";
import Footer from "~/components/Footer";
export default {
  name: "default",
  components: {Footer, Header}
}
</script>

<style scoped>

</style>
