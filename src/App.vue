<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router';
import HeaderView from './views/HeaderView.vue';
import FooterView from './views/FooterView.vue';
</script>

<template>
  <img alt="bg" class="bg" src="@/assets/bg.png" />
  <div class="mainPage">
    <header>
      <img alt="logo" class="logo" src="@/assets/logo.png" height="160" />
      <div>
        <HeaderView title_1="可汗杯" title_2="萨卡兹肉鸽赛季" />

        <nav class="links">
          <RouterLink to="/">分数计算器</RouterLink>
          <RouterLink to="/rules">比赛规则</RouterLink>
        </nav>
      </div>
    </header>

    <RouterView />
    <FooterView />
  </div>
</template>

<style scoped>
.bg {
  position: fixed;
  top: 0;
  left: 0;
  min-width: 100%;
  z-index: -1;
  opacity: 0.5;
}

.mainPage {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

header {
  display: flex;
  flex-direction: row;
  margin-top: 3rem;
}

.logo {
  margin-right: -5rem;
}

.links {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
  font-weight: 700;
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  nav {
    text-align: left;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
