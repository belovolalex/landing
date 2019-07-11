<template lang="pug">
    div
      header-layout
      flyer-comp
      footer-layout
</template>

<script>
import HeaderLayout from '../layouts/HeaderLayout'
import FlyerComp from '../components/FlyerComp'
import FooterLayout from '../layouts/FooterLayout'

export default {
  components: {
    HeaderLayout,
    FlyerComp,
    FooterLayout
  }
};
</script>

<style>
</style>
