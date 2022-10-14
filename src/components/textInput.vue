<template>
  <input type="text" placeholder="分数以空格间隔 如 90 90 89" />
</template>

<script setup lang="ts">
</script>
<style scoped>
input {
  width: 100%;
  height: 3rem;
  line-height: 3rem;
  padding: 0.1rem 0;
  color: #fff;
  border: none;
  border-bottom: 1px solid #fff;
  margin-bottom: 2rem;
  background: transparent;
  font-size: 1.5rem;
}
input::placeholder {
  color: #177276;
  font-size: 1.2rem;
}
</style>
