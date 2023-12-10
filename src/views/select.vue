<template>
  <div class="select">
    <button @click="back">返回</button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
const router = useRouter()
const back = () => {
    router.back()
}
</script>
<style lang="scss">
</style>