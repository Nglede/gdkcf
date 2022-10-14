<script setup lang="ts">
import { ref, Ref } from 'vue';
import Button from './components/Button.vue';


interface suject {
  score: number,
  credit: number
}

const courseList = ['必修', '选修']
const creditList = [0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 4.5]

const score = ref('')
const courseSelected = ref('必修')
const creditSelected = ref('1')
const bxArr = ref<suject[]>([])
const xxArr = ref<suject[]>([])

const bxScore = ref<number>(0)
const xxScore = ref<number>(0)
const bxCredit = ref<number>(0)
const xxCredit = ref<number>(0)
const res = ref<number>(0)

// 判断 必修/选修
const addSuject = (courseArr: Ref<suject[]>, arr: suject[]): void => {
  if (courseArr.value === void 0) {
    courseArr.value = [...arr]
  } else {
    courseArr.value = courseArr.value.concat(arr)
  }
}

// 计算 成绩 * 学分 之和
const calSujectSum = (arr: suject[]): number => {
  let res = 0
  arr.forEach(item => {
    res += item.score * item.credit
  })
  return res
}

// 计算学分和
const calCreditSum = (arr: suject[]): number => {
  let res = 0
  arr.forEach(item => {
    res += item.credit
  })
  return res
}

// 计算课程分
const calReslust = (): number => {
  console.log(xxArr.value.length);

  let res = 0
  bxScore.value = calSujectSum(bxArr.value)
  bxCredit.value = calCreditSum(bxArr.value)
  if (xxArr.value.length) {
    xxScore.value = calSujectSum(xxArr.value)
    xxCredit.value = calCreditSum(xxArr.value)

    let bxTemp = (bxScore.value / bxCredit.value)
    let xxTemp = (xxScore.value / xxCredit.value)
    bxTemp = Math.floor(bxTemp * 100) / 100
    xxTemp = Math.floor(xxTemp * 100) / 100

    res = bxTemp * 0.85 + xxTemp * 0.15
  } else {
    let bxTemp = (bxScore.value / bxCredit.value)
    bxTemp = Math.floor(bxTemp * 100) / 100
    res = bxTemp
  }
  return res
}

// 添加
const submit = () => {
  if (score.value === '') return
  const scoreArr = score.value.split(' ')

  const tempArr = scoreArr
    .filter(item => !!item)
    .map(item => {
      return {
        score: Number(item),
        credit: Number(creditSelected.value)
      }
    })

  if (courseSelected.value === '必修') {
    addSuject(bxArr, tempArr)
  } else {
    addSuject(xxArr, tempArr)
  }

  res.value = calReslust()
  console.log('res', res.value);

  score.value = ''
}

// 清空所有
const clear = () => {
  bxArr.value = []
  xxArr.value = []
  bxScore.value = 0
  bxCredit.value = 0
  xxScore.value = 0
  xxCredit.value = 0
  res.value = 0
}

</script>

<template>
  <div class="app">
    <h1>课 程 分</h1>
    <div class="content">
      <div class="header">
        <div class="select">
          <select v-model="courseSelected">
            <option :value="item" v-for="item in courseList">{{ item }}</option>
          </select>
          <select v-model="creditSelected">
            <option :value="item" v-for="item in creditList">{{ item }}</option>
          </select>
        </div>
        <Button @click="submit">确定</Button>
      </div>
      <input type="text" name="input" v-model="score" placeholder="分数以空格间隔 如 90 90 89" />
      <!-- <textInput v-model="score"></textInput> -->
      <div class="record">
        <Button v-if="bxArr || xxArr" @click="clear">重置</Button>
      </div>
      <div class="reslust">
        <div class="text">{{ res }}</div>
      </div>
    </div>
  </div>

  <div class="footer">
    Powered by
    <a href="https://webify.cloudbase.net/" target="_blank" rel="noopener noreferrer">CloudBase Webify</a>
  </div>
</template>

<style>
body {
  font-family: sans-serif;
  background: linear-gradient(#141e30, #243b55);
}

.app {
  margin: 5rem auto 0;
  width: 60%;
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(0, 0, 0, 0.5);
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.6);
  border-radius: 10px;
}

.app h1 {
  margin: 2rem 0 4rem 0;
  font-size: 2.5rem;
  color: #03e9f4;
}

.content {
  min-height: 30vh;
  width: 60%;
  max-width: 70vw;
  display: flex;
  flex-direction: column;
}

.content .header {
  margin: 1rem 0 0.5rem;
  display: flex;
  justify-content: space-between;
}

.content input {
  width: 100%;
  height: 3rem;
  line-height: 3rem;
  padding: 0.1rem 0;
  color: #fff;
  border: none;
  border-bottom: 1px solid #fff;
  background: transparent;
  font-size: 1.5rem;
}

input::placeholder {
  color: #177276;
  font-size: 1.2rem;
}

.header .select select {
  width: 3.5rem;
  height: 2rem;
  line-height: 2rem;
  text-align: center;
  font-weight: 600;
  font-size: 1rem;
}

select+select,
.button+.button {
  margin-left: 1rem;
}

.record {
  margin-top: 1.5rem;
  display: flex;
  flex-direction: row;
}

.reslust {
  margin-top: 1.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.reslust .text {
  /* margin-top: 1rem; */
  font-size: 4rem;
  font-weight: 500;
  color: #fff;
}

.reslust .details {
  cursor: pointer;
  text-decoration: underline;
}

.footer {
  color: #fff;
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
}

.footer a {
  text-decoration: none;
  background: linear-gradient(0.25turn, #0052d9, #00a4ff);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

.footer a:hover {
  text-decoration: underline;
  color: #4596b3;
}
</style>
