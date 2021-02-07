<template>
  <div>
    <img :src="logo" alt="logo">
    <Test />
  </div>
</template>

<script>
import Test from "components/Test";

import logo from 'img/favicon.png';

export default {
  components: {
    Test,
  },

  data() {
    return {
      logo,
    };
  },
}
</script>

<style lang="sass">
@use 'styles'
</style>
