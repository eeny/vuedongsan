<template>
    <div class="black-bg" v-if="modalIsOpen">
    <div class="white-bg">
      <h4>{{ oneRooms[selNum].title }}</h4>
      <img :src="oneRooms[selNum].image" class="room-img">
      <p>{{ oneRooms[selNum].content }}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <input v-model="month">
      <!-- textarea, input, select, checkbox 등 다양한 input에 v-model 가능 -->
      <!-- 사용자가 input에 입력한 값은 문자자료형이므로 숫자타입이라고 지정하려면 v-model.number로 기재하면 됨 -->
      <p> {{ month }}개월 선택함 : {{ oneRooms[selNum].price * month }}원</p>
      <!-- <button @click="modalIsOpen = false">X</button>props로 받아온 데이터는 재할당 불가능 -->
      <button @click="$emit('closeModal')">X</button>
    </div>
  </div>
</template>

<script>
export default {
    name: 'ModalComp',
    data() {
      return {
        month : 1,
      }
    },
    beforeUpdate() {
      if (this.month == 2) {
        alert('2개월 불가');
        this.month = 1;
      }
    },
    watch: {
      // afterData 변경후 데이터, beforeData 변경전 데이터
      // 보통은 afterData 변수 1개만 적으면 됨
      month(afterData) {
        // 사용자가 month를 글자로 입력한 데이터가 13보다 크면 경고문 띄우기
        if(afterData >= 13) {
          alert('13이상 큰 숫자 입력 불가');
          this.month = 1;
        }
        if (isNaN(afterData)) {
          alert('문자열 포함됨');
          this.month = 1;
        }
        
      },
    },
    props: {
        oneRooms : Array,
        selNum : Number,
        modalIsOpen : Boolean,
    }
}
</script>

<style>

</style>