<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <div class="headerView">
    <h1>{{ title }}</h1>
    <h3>
      活动策划：
      <a href="https://space.bilibili.com/122574257" target="_blank" rel="noopener">B站@你有五根棒棒糖嘛w</a>
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.8rem;
  font-family: "方正特雅宋_GBK";
}

h3 {
  font-size: 1.2rem;
  font-family: '华文仿宋';
  font-weight: 700;
}

.headerView {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vh;
}

.headerView h1,
.headerView h3 {
  text-align: center;
  writing-mode: horizontal-tb;
}

@media (min-width: 1024px) {

  .headerView h1,
  .headerView h3 {
    text-align: left;
  }
}
</style>
