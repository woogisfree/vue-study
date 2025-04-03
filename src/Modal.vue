<template>
  <div class="black-bg" v-if="모달창열렸니">
    <div class="white-bg">
      <Discount />
      <img :src="원룸들[누른거].image" style="width: 100%" />
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <input v-model="month" />
      <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
import Discount from './DiscountBanner.vue';

export default {
  name: 'Modal',
  data() {
    return {
      month: 1,
    };
  },
  watch: {
    // watch: { 감시할데이터() {} } - 감시할데이터가 변경될 때마다 watcher 실행됨
    month(a) {
      if (isNaN(a)) {
        alert('숫자만 입력해');
        this.month = 1;
      }
    },
  },
  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
  components: {
    Discount,
  },
};
</script>

<style></style>
