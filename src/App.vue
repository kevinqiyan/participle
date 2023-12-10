<template>
  <div class="main" v-show="inputShow">
    <textarea v-model="text" cols="50" maxlength="1000" />
    <!-- <router-view></router-view> -->
  </div>
  <ul class="list" v-show="!inputShow">
    <li class="item" v-for="(item, index) in txt" :key="index">{{ item }}</li>
  </ul>
  <footer>
    <div class="button" @click="clear" v-show="inputShow">清空文本</div>
    <div class="button" @click="splitFn" v-show="inputShow">点击分词</div>
    <div class="button" @click="back" v-show="!inputShow">返回</div>
  </footer>
</template>
<script setup>
import { Segment, useDefault } from 'segmentit'
import { ref } from 'vue'
const text = ref('')
const txt = ref([])
const inputShow = ref(true)
const segmentit = useDefault(new Segment())

const splitFn = () => {
  if (!text.value || !text.value?.trim()) {
    alert('请输入文本')
    return
  }
  const result = segmentit.doSegment(text.value)
  txt.value = result.map((word) => word.w)
  inputShow.value = false
}
const clear = () => {
  text.value = ''
  txt.value = []
}

const back = () => {
  inputShow.value = true
}
</script>

<style lang="scss">
.main {
  height: 90vh;
  overflow: hidden;
  position: relative;
  textarea {
    width: 100%;
    height: 90vh;
    resize: none;
  }
}
.list {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  .item {
    min-width: 100px;
    width: auto;
    border: 1px solid rgba(64, 64, 218, 0.6);
    color: rgb(64, 64, 218);
    text-align: center;
    line-height: 20px;
    font-size: 12px;
    margin: 10px;
    padding: 5px 8px;
    border-radius: 6px;
    transition-property: all; /* 指定要应用过渡效果的属性 */
    transition-duration: 0.2s; /* 过渡持续时间为2秒 */
    transition-timing-function: ease; /* 过渡函数为ease（默认值）*/
    transition-delay: 0s; /* 延迟3秒开始过渡效果 */
    &:hover {
      background: #bfa;
      cursor: pointer;
      transform: scale(1.2, 1.2);
    }
  }
}

footer {
  height: 40px;
  width: 100%;
  position: fixed;
  bottom: 10px;
  right: 10px;
  display: flex;
  flex-direction: row;
  justify-content: end;
  .button {
    width: 120px;
    height: 40px;
    text-align: center;
    line-height: 40px;
    background: rgb(57, 149, 251);
    font-size: 14px;
    color: #fff;
    margin-left: 5px;
    &:hover{
      background: rgba(57, 149, 251,0.8);
      color: #fff;
      cursor: pointer;
    }

  }
}
</style>
