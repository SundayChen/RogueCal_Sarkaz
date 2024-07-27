<script setup lang="ts">
import type { Team } from '../../views/ScoreBoard.vue'
import './scorePart.css'
defineProps<{
    item: Team;
}>()
</script>

<template>
    <div class="wrapper">
        <h2 class="title">得分详情</h2>
        <div class="newLine">
            <div class="row_part">
                <p>讲述者：</p>
                <img :src="`/${item.name}_speed.jpg`" alt="img" width="60" />
                <p class="item">{{ item.speed_player }}</p>
            </div>
            <div class="row_part">
                <div class="col_part">
                    <p>结算分</p>
                    <p class="item">{{ item.speed_settlement }}</p>
                </div>
                <div class="col_part">
                    <p>用时</p>
                    <p class="item">{{ item.speed_time }}</p>
                </div>
            </div>
        </div>
        <div class="newLine">
            <p>开局分队：<span class="item">{{ item.speed_startTeam }}</span></p>
            <p>开局主力：<span class="item">{{ item.speed_startOperator }}</span></p>
        </div>
        <div class="newLine">
            <div class="row_part">
                <p>完成结局：{{ item.speed_end.length > 0 ? '' : '-' }}</p>
                <img v-if="item.speed_end.length > 0" v-for="end in item.speed_end" :src="`/end${end}.png`" alt="img"
                    width="80" />
            </div>
            <div class="col_part">
                <p>最终得分</p>
                <p class="final">{{ item.speed_score }}</p>
            </div>
        </div>
    </div>
</template>