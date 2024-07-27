<script setup lang="ts">
defineProps<{
  title_1: string
  title_2: string
}>()
</script>

<template>
  <div class="headerView">
    <h1><span class="yellow">{{ title_1 }}</span>{{ ' ' }}{{ title_2 }}</h1>
    <h3>
      活动策划：
      <a href="https://space.bilibili.com/122574257" target="_blank" rel="noopener">B站@你有五根棒棒糖嘛w</a>
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 3rem;
  font-family: "my-fztys";
  margin-left: 4rem;
}

.yellow {
  color: #ffa000;
}

h3 {
  font-size: 1.2rem;
  font-family: 'my-hwfs';
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
