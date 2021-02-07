<template>
  <div>
    <span class="test">Test</span>
    <button @click.stop="test"></button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isValid: true,
      testValue: 1,
    };
  },
  methods: {
    test(event) {
      this.isValid ? this.testValue = 0 : event.preventDefault();
      console.log(this.testValue);
    },
  },
}
</script>
