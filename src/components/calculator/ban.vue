<script setup lang="ts">
import { ref, computed } from 'vue'
import './calculatorPart.css'

const ban_operator = ref<boolean[]>([false, false, false, false, false, false, false, false])

const ban_blueprint = ref<boolean>(false);
const ban_noRetry = ref<boolean>(false);

const ban_tempSix = ref<number>(0);
const ban_tempFive = ref<number>(0);
const ban_tempFour = ref<number>(0);
const ban_isBossAltered = ref<boolean>(false);
const ban_secondEnding = ref<boolean>(false);
const ban_thirdEnding = ref<boolean>(false);
const ban_settlement = ref<number>(0);

const ban_finalScore = computed(() => {
    const this_score = ban_tempSix.value * 50 + ban_tempFive.value * 20 + ban_tempFour.value * 10
        + (ban_isBossAltered.value ? 50 : 0) + (ban_secondEnding.value ? 100 : 0) + (ban_thirdEnding.value ? 200 : 0) +
        ((ban_secondEnding.value && ban_thirdEnding.value) ? 100 : 0) +
        ban_operator.value.reduce((acc, cur) => acc + (cur ? 50 : 0), 0) +
        (ban_blueprint.value ? 100 : 0) + (ban_noRetry.value ? 50 : 0) + ban_settlement.value;
    return this_score;
})

const profession = ['先锋', '近卫', '重装', '狙击', '术师', '医疗', '辅助', '特种'];
</script>

<template>
    <div class="calWrapper">
        <h2 class="calTitle">自限模式</h2>
        <div style="display: flex; flex-direction: row; gap: 4rem;">
            <div class="banWrapper">
                <div>
                    <p>临时招募六星</p>
                    <input v-model="ban_tempSix" type="number" min="0" class="numberInput" />
                </div>
                <div>
                    <p>临时招募五星</p>
                    <input v-model="ban_tempFive" type="number" min="0" class="numberInput" />
                </div>
                <div>
                    <p>临时招募四星</p>
                    <input v-model="ban_tempFour" type="number" min="0" class="numberInput" />
                </div>
                <div class="row_item">
                    <input v-model="ban_isBossAltered" type="checkbox" />
                    <p>三层BOSS异格</p>
                </div>
                <div class="row_item">
                    <input v-model="ban_secondEnding" type="checkbox" />
                    <p>完成二结局</p>
                </div>
                <div class="row_item">
                    <input v-model="ban_thirdEnding" type="checkbox" />
                    <p>完成三结局</p>
                </div>
                <div class="row_item">
                    <input v-model="ban_blueprint" type="checkbox" />
                    <p>未使用蓝图测绘分队</p>
                </div>
                <div class="row_item">
                    <input v-model="ban_noRetry" type="checkbox" />
                    <p>未使用重开机会</p>
                </div>
            </div>
            <div class="banWrapper">
                <div v-for="(item, index) in ban_operator" :key="index" class="row_item">
                    <input :checked="item" @click="ban_operator[index] = !ban_operator[index]" type="checkbox" />
                    <p>{{ profession[index] }}自限</p>
                </div>
            </div>
        </div>
        <div class="scoresDisplay">
            <div>
                <p>结算分数</p>
                <input v-model="ban_settlement" type="number" min="0" class="numberInput" />
            </div>
            <div>
                <p>最终分数</p>
                <p class="finalScore
                ">{{ ban_finalScore }}</p>
            </div>
        </div>
    </div>
</template>
