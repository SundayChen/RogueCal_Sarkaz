<script setup lang="ts">
import { ref, computed } from 'vue'
import './calculatorPart.css'

const speed_prevScore = ref<number>(0)
const speed_notFinish = ref<boolean>(false)
const speed_hours = ref<number>(0)
const speed_minutes = ref<number>(0)
const speed_seconds = ref<number>(0)
const speed_settlement = ref<number>(0)

const speed_finalScore = computed(() => {
  let this_score = 0;
  if (speed_notFinish.value)
    this_score = speed_settlement.value > 2400 ? 2400 : speed_settlement.value;
  else {
    this_score = 6000 - (speed_hours.value * 3600 + speed_minutes.value * 60 + speed_seconds.value) * 2;
    this_score = this_score < 2400 ? 2400 : this_score;
  }

  return this_score > speed_prevScore.value ? this_score : speed_prevScore.value;
})
</script>

<template>
  <div class="calWrapper">
    <h2 class="calTitle">速通模式</h2>
    <div>
      <p>上次速通得分</p>
      <input v-model="speed_prevScore" type="number" min="0" class="numberInput" />
    </div>
    <p>本次速通用时</p>
    <div class="row_item">
      <input v-model="speed_hours" type="number" min="0" class="numberInput" />
      <span style="font-size: 1rem;"> ： </span>
      <input v-model="speed_minutes" type="number" max="59" min="0" class="numberInput" />
      <span style="font-size: 1rem;"> ： </span>
      <input v-model="speed_seconds" type="number" max="59" min="0" class="numberInput" />
    </div>
    <div class="row_item">
      <input v-model="speed_notFinish" type="checkbox" />
      <p>未完成结局</p>
    </div>
    <div class="scoresDisplay">
      <div>
        <p>结算分数</p>
        <input v-model="speed_settlement" type="number" min="0" class="numberInput" />
      </div>
      <div>
        <p>最终分数</p>
        <p class="finalScore">{{ speed_finalScore }}</p>
      </div>
    </div>
  </div>
</template>