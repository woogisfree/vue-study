<template>
  <Transition name="fade">
    <Modal
      @closeModal="모달창열렸니 = false"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </Transition>

  <div class="menu">
    <a v-for="(a, i) in menus" :key="i">{{ a }}</a>
  </div>

  <Discount v-if="showDiscount == true" :amount="amount" />
  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    @openModal="
      모달창열렸니 = true;
      누른거 = $event;
    "
    :room="원룸들[i]"
    v-for="(원룸, i) in 원룸들"
    :key="원룸"
  />
</template>

<script>
import data from './assets/oneroom.js';
import CardComp from './CardComp.vue';
import Discount from './DiscountBanner.vue';
import Modal from './Modal.vue';

export default {
  name: 'App',
  data() {
    return {
      // Define any data properties here
      amount: 30,
      showDiscount: true,
      원룸들오리지널: [...data],
      누른거: 0,
      원룸들: [...data],
      모달창열렸니: false,
      신고수: [0, 0, 0, 0, 0, 0],
      menus: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
    };
  },
  mounted() {
    this.startDiscountTimer();
  },
  methods: {
    // Define any methods here
    increase() {
      this.신고수[0]++;
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
    priceSort() {
      this.원룸들.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    startDiscountTimer() {
      const timer = setInterval(() => {
        if (this.amount > 0) {
          this.amount--;
        } else {
          clearInterval(timer);
          this.showDiscount = false;
        }
      }, 1000);
    },
  },

  components: {
    Discount,
    Modal,
    Card: CardComp,
  },
};
</script>

<style>
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}

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
