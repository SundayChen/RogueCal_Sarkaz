<script setup lang="ts">
import Ban from '@/components/calculator/ban.vue';
import Normal from '@/components/calculator/normal.vue';
import Speed from '@/components/calculator/speed.vue';
import { ref } from 'vue';

const normalScore = ref<number>(0);
const speedScore = ref<number>(0);
const banScore = ref<number>(0);
</script>

<template>
  <div class="homeWrapper">
    <Normal />
    <Speed />
    <Ban />
  </div>
</template>

<style scoped>
.homeWrapper {
  display: flex;
  flex-direction: row;
  gap: 2rem;
}
</style>