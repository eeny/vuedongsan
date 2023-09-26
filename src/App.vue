<template>

  <!-- <div v-if="1 == 2">
    Hi!
  </div>
  <div v-else-if="1 == 1">
    Bye!
  </div>
  <div v-else>
    Bye Bye~
  </div> -->

  <!-- <div class="start" :class="{ end : modalIsOpen  }"> -->
  <transition name="fade">
    <Modal @closeModal="modalIsOpen = false;" :oneRooms = "oneRooms" :selNum = "selNum" :modalIsOpen = "modalIsOpen" />
    <!-- </div> -->
  </transition>
  
  <div class="menu">
    <a v-for="menuItem in menus" :key="menuItem">{{ menuItem }}</a>
  </div>

  <Discount v-if="showDiscount == true"/>
  <!-- <Discount></Discount> -->

  <button @click="priceLowSort">가격낮은정렬</button>
  <button @click="priceHighSort">가격높은순정렬</button>
  <button @click="titleSort">상품명 가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card @openModal="modalIsOpen = true; selNum = $event" :oneRooms = "oneRooms" :fontcolor = "fontcolor" :obj = "obj" />

</template>

<script>
import roomData from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){
    return {
      price : [80, 70, 90],
      fontcolor : ['color: blue', 'color: red', 'color: orange', 'color: purple', 'color: magenta', 'color: aqua'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
      menus : ['Home', 'Shop', 'About'],
      count : [0, 0, 0],
      modalIsOpen: false, // 현재 모달창 UI 상태 저장
      oneRoomsOrigin : [...roomData],  // 원본데이터 보존(array 및 object 데이터의 별개 사본을 만드는 방법)
      oneRooms : roomData,
      selNum : 0,
      obj : { name : 'kim', age : 20 },
      showDiscount : true,
    }
  },
  methods: {
    increase(i){
      this.count[i]++;
    },
    priceLowSort(){
      this.oneRooms.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceHighSort(){
      this.oneRooms.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    titleSort(){
      this.oneRooms.sort(function (a, b) {
        if(a.title > b.title) return 1;
        if(a.title < b.title) return -1;
        return 0;
      });
    },
    sortBack(){
      // = 등호로 Array를 집어넣으면 좌 우 값을 공유하게 됨
      // this.oneRooms = this.oneRoomsOrigin;
      this.oneRooms = [...this.oneRoomsOrigin];
    }
  },
  // // LifeCycle Hook 사용하기(beforeMount, created, updated, ...)
  // created() {
  //   // 서버에서 데이터가져오는 코드~ ajax 요청시 create 또는 mounted 중에서 주로 요청한다
  // },
  // mounted() {
  //   setTimeout(() => {
  //     this.showDiscount = false;
  //   }, 2000);
  // },
  components: {
    Discount : Discount,  // 왼쪽 오른쪽 동일한 경우 Discount 로만 적는 거 가능
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.fate-leave-from {
  opacity: 0;
}

.fade-enter-from {
  /* opacity: 0; */
  transform: translateY(-1000px);
}

.fade-enter-active{
  transition: all 1s;
}

.fade-enter-to {
  /* opacity: 1; */
  transform: translateY(0px);
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}

.black-bg {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top:  10px;
}
</style>
