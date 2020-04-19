<!--follow pages: https://juejin.im/post/5e99c21b6fb9a03c590dfea8#heading-8-->
<!-- ctx ref watch router vuex event-->
<template>
  <div class="test">
    <h1>test count: {{count}}</h1>
    <div>count * 2 = {{doubleCount}}</div>
    <div>state from vuex {{a}}</div>
    <button @click="add">add</button>
    <button @click="update">update a</button>
  </div>
</template>

<script>
import {
  ref, watch, computed, getCurrentInstance,
} from 'vue';

export default {
  setup() {
    const { ctx } = getCurrentInstance();
    console.log(ctx.$router.currentRoute.value);

    const count = ref(0);
    const add = () => {
      count.value += 1;
    };

    watch(() => count.value, (val) => {
      console.log(`count is ${val}`);
    });

    const doubleCount = computed(() => count.value * 2);

    const a = computed(() => ctx.$store.state.test.a);

    const update = () => {
      ctx.$store.commit('setTestA', count);
    };

    return {
      count,
      doubleCount,
      add,
      update,
      a,
    };
  },
};
</script>
