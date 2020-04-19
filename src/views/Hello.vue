<!-- follow pages: https://juejin.im/post/5e13ecbe6fb9a04846508ab2#heading-0-->
<!-- setup reactive ref toRefs watchEffect-->
<template>
  <div>
    <input type="text" v-model="state.value"> {{ state.value}}
    <test-com title="hello world"></test-com>
    <br>

    <div>
      count: {{ count }}
      <button @click="handlerCountAdd">click ++</button>
    </div>
    <br>

    <div>
      <input type="text" v-model="inputValue">
      <br>
      rvalue: {{rvalue}}
    </div>
  </div>
</template>

<script>
import {
  reactive, toRefs, computed, watch, watchEffect,
} from 'vue';
import TestCom from '../components/TestCom.vue';

export default {
  name: 'Hello',
  components: { TestCom },
  setup(props, ctx) {
    // reactive 是包装整个对象
    // ref是包装单个值
    // 因此单个包装可以直接return，而多个包装可以通过toRefs结构成单个，或者通过state来访问

    const state = reactive({ value: '' });
    console.log(props, ctx);

    const countState = reactive({ count: 1 });
    const handlerCountAdd = () => {
      countState.count += 1;
    };


    const inputState = reactive({
      inputValue: '',
      rvalue: computed(() => inputState.inputValue.split('').reverse().join('')),
    });

    watch(() => inputState.inputValue, (val) => {
      console.log('val', val);
    });

    // 根据输出的内容的个数决定输出的次数
    watchEffect(() => {
      console.log('effect', inputState.inputValue);
      console.log('effect', countState.count);
    });

    return {
      state, ...toRefs(countState), handlerCountAdd, ...toRefs(inputState),
    };
  },
};
</script>

<style scoped>

</style>
