<template>
  <div>
    <div class="div">疯狂追求者</div>
    <MySecond @apply="applyFriend" :tag="AgreeFlag" :countNum="count"></MySecond>
    <br />
    <div class="container-box">
      <p>男生发送爱心数 <span>{{ count }}</span></p>
      <button v-if="isShowA" @click="addHeartNum">增加心数</button>
      <button v-if="isShowF" @click="applySend('f')">申请做女朋友</button>
      <button v-if="isShowM" @click="applySend('m')">申请求婚</button>
      <button v-if="isShowP" @click="applySend('p')">申请分手</button>
    </div>


  </div>
</template>

<script>
import mySecond from './mySecond.vue';
export default {
  components: {
    MySecond: mySecond
  },
  data() {
    return {
      count: 0,
      isShowF: false,
      isShowM: false,
      isShowP: false,
      isShowA: true,
      AgreeFlag: ''
    }
  },
  methods: {
    addHeartNum() {
      // if(this.count >= 25) {
      //   alert('你以经爱她爱的不能自拔了,请求她嫁你吧')
      //   this.count = 25
      // } else if(this.count == 17) {
      //   alert('你与她的关系已经很好,可以请求她做你的女朋友了')
      //   this.count ++
      // } else {
      //   this.count ++
      // }
      this.count++

    },
    applySend(tag) {
      this.AgreeFlag = tag + new Date().getTime()
      this.isShowF = false
      this.isShowM = false
      this.isShowP = false
    },
    applyFriend(i) {
      if (i === 1) {
        this.isShowF = true
      } else if (i === 2) {
        this.isShowM = true
      } else if (i === 3) {
        this.isShowP = true
      } else if (i === 4) {
        this.isShowA = false
      }


    },

  }
}
</script>

<style scoped lang="less">
.div {
  color: red;
}

.container-box {
  background: #f0f;
}
</style>