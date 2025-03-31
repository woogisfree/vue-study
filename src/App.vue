<template>
  <div class="black-bg" v-if="모달창열렸니">
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지내용임</p>
      <button @click="모달창열렸니 = false">닫기</button>
    </div>
  </div>

  <div class="menu">
    <a v-for="(a, i) in menus" :key="i">{{ a }}</a>
  </div>

  <div v-for="(room, i) in 원룸들" :key="i">
    <img :src="room.image" class="room-img" />
    <h4 @click="모달창열렸니 = true">{{ room.title }}</h4>
    <p>{{ room.price }}원</p>
    <button @click="신고수[i]++">허위매물신고</button>
    <span> 신고수 : {{ 신고수[i] }}</span>
  </div>
</template>

<script>
import data from './assets/oneroom.js';

export default {
  name: 'App',
  data() {
    return {
      // Define any data properties here
      원룸들: data,
      모달창열렸니: false,
      신고수: [0, 0, 0, 0, 0, 0],
      menus: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
    };
  },
  methods: {
    // Define any methods here
    increase() {
      this.신고수[0]++;
    },
  },
  components: {},
};
</script>

<style scoped>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .menu {
    background: darkslateblue;
    padding: 15px;
    border-radius: 5px;
  }

  .menu a {
    color: white;
    padding: 10px;
  }
}
</style>
