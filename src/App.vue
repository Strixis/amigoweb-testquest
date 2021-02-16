<template>
  <div class="container">
    <RegistrationForm />
  </div>
</template>

<script>
import RegistrationForm from "components/RegistrationForm";

import logo from 'img/favicon.png';

export default {
  components: {
    RegistrationForm,
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
