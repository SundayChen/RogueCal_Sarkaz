<script setup lang="ts">
import { ref, computed } from 'vue'
import './calculatorPart.css'

const normal_prevScore = ref<number>(0)
const normal_tempSix = ref<number>(0)
const normal_tempFive = ref<number>(0)
const normal_tempFour = ref<number>(0)
const normal_isBossAltered = ref<boolean>(false)
const normal_secondEnding = ref<boolean>(false)
const normal_thirdEnding = ref<boolean>(false)
const normal_settlement = ref<number>(0)

const normal_finalScore = computed(() => {
    const this_score = normal_tempSix.value * 50 + normal_tempFive.value * 20 + normal_tempFour.value * 10
        + (normal_isBossAltered.value ? 50 : 0) + (normal_secondEnding.value ? 100 : 0) + (normal_thirdEnding.value ? 200 : 0) +
        ((normal_secondEnding.value && normal_thirdEnding.value) ? 100 : 0) + normal_settlement.value;
    return this_score > normal_prevScore.value ? this_score : normal_prevScore.value;
})
</script>

<template>
    <div class="calWrapper">
        <h2 class="calTitle">普通模式</h2>
        <div>
            <p>之前最高分</p>
            <input v-model="normal_prevScore" type="number" min="0" class="numberInput" />
        </div>
        <div>
            <p>临时招募六星</p>
            <input v-model="normal_tempSix" type="number" min="0" class="numberInput" />
        </div>
        <div>
            <p>临时招募五星</p>
            <input v-model="normal_tempFive" type="number" min="0" class="numberInput" />
        </div>
        <div>
            <p>临时招募四星</p>
            <input v-model="normal_tempFour" type="number" min="0" class="numberInput" />
        </div>
        <div class="row_item">
            <input v-model="normal_isBossAltered" type="checkbox" />
            <p>三层BOSS异格</p>
        </div>
        <div class="row_item">
            <input v-model="normal_secondEnding" type="checkbox" />
            <p>完成二结局</p>
        </div>
        <div class="row_item">
            <input v-model="normal_thirdEnding" type="checkbox" />
            <p>完成三结局</p>
        </div>
        <div class="scoresDisplay">
            <div>
                <p>结算分数</p>
                <input v-model="normal_settlement" type="number" min="0" class="numberInput" />
            </div>
            <div>
                <p>最终分数</p>
                <p class="finalScore">{{ normal_finalScore }}</p>
            </div>
        </div>
    </div>
</template>