<template>
    <div>hello test child com</div>
</template>

<script>
export default {
  name: 'TestCom',
  setup(props, ctx) {
    console.log('testcom', props, ctx);
  },
};
</script>

<style scoped>

</style>
