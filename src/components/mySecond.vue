<template>
    <div class="container">
        <p><span>美女的心动指数</span></p>
        <p><span>{{ heartIndex.toFixed(1) }}</span></p>
        <p v-if="girlState.isBegirlfriend">是否同意做女朋友<button @click="isAgree('ag')">同意</button><button
                @click="isAgree('disag')">不同意</button></p>
        <p v-if="girlState.isAgreeMarried">是否同意结婚 <button @click="isAgree('mar')">同意</button><button
                @click="isAgree('rej')">不同意</button></p>
        <p v-if="girlState.isAgreeParted">是否同意分手 <button @click="isAgree('agrP')">同意</button></p>
    </div>
</template>

<script>
export default {
    props: ['countNum', 'tag'],
    data() {
        return {
            girlState: {
                isBegirlfriend: false,
                isAgreeMarried: false,
                isAgreeParted: false
            },
            applyTimes: {
                friend: 0,
                wife: 0
            },
            heartIndex: 10

        }
    },
    watch: {
        countNum() {
            let addNum = Math.floor(Math.random() * 10) / 10
            this.heartIndex = this.heartIndex + addNum
            let count = this.heartIndex
            console.log(addNum)
            if (count >= 26) {
                this.heartIndex++
                alert('你们开心的生活在一起了,让我们荡起双桨,小船儿吹开波浪')
            } else if (count >= 25 && count <= 26) {
                this.heartIndex++
                // this.girlState.isAgreeMarried = true
                alert('她应该很爱你了,请求她嫁给你吧')
                this.$emit('apply', 2)
            } else if (count <= 19 && count >= 17) {
                // this.girlState.isBegirlfriend = true
                alert('她可能爱上你了,请求她作为你的女朋友吧')
                this.$emit('apply', 1)
                this.heartIndex =this.heartIndex +1
            } else if (count < 15    && count >14) {
                this.heartIndex ++
                alert('她在慢慢喜欢你哦,加油哦')
            }else {
                Object.keys(this.girlState).forEach(keys => {
                    this.girlState[keys] = false
                }
                )
            }
        },
        tag() {
            if (!this.tag) return
            let tag = this.tag.substr(0, 1)
            if (tag === 'f') {
                this.girlState.isBegirlfriend = true
            } else if (tag === 'm') {
                this.girlState.isAgreeMarried = true
            } else if (tag === 'p') {
                this.girlState.isAgreeParted = true
            }
        }
    },
    methods: {
        isAgree(key) {
            var timesW = this.applyTimes.wife
            var times = this.applyTimes.friend
            switch (key) {
                case 'ag':
                    this.girlState.isBegirlfriend = false
                    this.heartIndex = this.heartIndex + 3
                    if (this.applyTimes.friend == 2) {
                        alert('不容易啊,终于弄到手了,你们恋爱了,要甜甜蜜蜜啊,加油要继续努力哦')
                    } else {
                        alert('你们恋爱了,要甜甜蜜蜜啊,加油要继续努力哦')
                    }
                    break;
                case 'disag':
                    this.girlState.isBegirlfriend = false
                    if (times <= 2) {
                        this.heartIndex = this.heartIndex - parseInt(Math.random() * 10 + 3)
                        this.applyTimes.friend++
                        alert('她还是不喜欢你了,你要加油哦')
                    } else {
                        this.$emit('apply', 3)
                        this.$emit('apply',4)
                        alert('她不可能再喜欢你了,你没戏了,换个姑娘吧,申请分手吧')
                        this.heartIndex = 0
                        
                    }
                    break;
                case 'mar':
                    this.girlState.isAgreeMarried = false
                    this.heartIndex = 30
                    if (timesW == 2) {
                        alert('千里长跑,终成伴侣,恭喜你们结婚了!要幸福哦')
                    } else {
                        alert('她同意和你结婚了,恭喜你们结婚了!要幸福哦')
                    }
                    break;
                case 'rej':
                    this.girlState.isAgreeMarried = false
                    if (timesW <= 2) {
                        this.heartIndex = this.heartIndex - parseInt(Math.random()*3)
                        this.applyTimes.wife++
                        alert('她不同意结婚,你要加油哦')
                    } else {
                        this.$emit('apply', 3)
                        this.$emit('apply',4)
                        alert('她不可能和你结婚了,你没戏了,换个姑娘吧,申请分手吧')
                        this.heartIndex = 0
                        
                    }
                    break;
                case 'agrP':
                    this.girlState.isAgreeParted = false
                    this.heartIndex = 0
                    alert('你们分手了,南辕北辙,各自安好')
                    this.$emit('apply',4)
                    break;
                
            }
        }
    }
}
</script>

<style>
.container {
    background: rgb(185, 185, 147);
}
</style>