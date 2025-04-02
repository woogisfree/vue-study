<template>
  <div class="black-bg" v-if="모달창열렸니">
    <div class="white-bg">
      <Discount />
      <img :src="원룸들[누른거].image" style="width: 100%" />
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <p>{{ 원룸들[누른거].price }}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
import Discount from './DiscountBanner.vue';

export default {
  name: 'Modal',
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
