<template>
    <div class="content">
      <Intro/>
      <Platforms/>
      <KeyFacts/>
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
  components: {KeyFacts, Platforms, Intro, Footer, Header}
}
</script>
