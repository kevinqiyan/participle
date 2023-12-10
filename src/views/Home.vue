<template>
  <div class="home">
    <input type="text" v-model="text">
  </div>
  <button @click="splitFn">点击分词</button>
</template>

<script setup>
import { Segment,useDefault } from 'segmentit';
import { ref } from 'vue';
import { useRouter } from 'vue-router'
const router = useRouter()
const text = ref('')
const txt = ref('')
const segmentit = useDefault(new Segment())


const splitFn = () => {
  if (!text.value || !text.value?.trim()) {
    alert('请输入文本')
    return
  }
  const result = segmentit.doSegment(text.value)
  txt.value = result.map(word => word.w)
}
</script>
<style>
</style>