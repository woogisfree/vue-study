<template>
  <div class="menu">
    <a v-for="(a, i) in menus" :key="i">{{ a }}</a>
  </div>

  <div>
    <h4>{{ products[0] }}</h4>
    <p>50 만원</p>
    <button @click="신고수[0]++">허위매물신고</button>
    <span> 신고수 : {{ 신고수[0] }}</span>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>70 만원</p>
    <button @click="신고수[1]++">허위매물신고</button>
    <span> 신고수 : {{ 신고수[1] }}</span>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>60 만원</p>
    <button @click="신고수[2]++">허위매물신고</button>
    <span> 신고수 : {{ 신고수[2] }}</span>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // Define any data properties here
      신고수: [0, 0, 0],
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
