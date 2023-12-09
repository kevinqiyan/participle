
<template>
  <div>
    <input type="text" v-model="text">
  </div>
<div>分词:{{ txt }}</div>
<button @click="splitFn">点击分词</button>
</template>
<script setup>
import { Segment,useDefault } from 'segmentit';
import { ref } from 'vue';
const text = ref('')
const txt = ref('')
const segmentit = useDefault(new Segment())


const splitFn = () => {
  if (!text.value || !text.value?.trim()) {
    alert('请输入文本')
    return
  }
  const result = segmentit.doSegment(text.value)
  txt.value = result
}
</script>

