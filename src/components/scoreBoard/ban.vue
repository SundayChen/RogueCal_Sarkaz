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
                <img :src="`/${item.name}_ban.jpg`" alt="img" width="60" />
                <p class="item">{{ item.ban_player }}</p>
            </div>
            <div class="row_part">
                <div class="col_part">
                    <p>结算分</p>
                    <p class="item">{{ item.ban_settlement }}</p>
                </div>
                <div class="col_part">
                    <p>额外分</p>
                    <p class="item">{{ item.ban_extra }}</p>
                </div>
            </div>
        </div>
        <div class="newLine">
            <p>开局分队：<span class="item">{{ item.ban_startTeam }}</span></p>
            <p>开局主力：<span class="item">{{ item.ban_startOperator }}</span></p>
        </div>
        <div class="newLine">
            <div class="row_part">
                <p>完成结局：{{ item.ban_end.length > 0 ? '' : '-' }}</p>
                <img v-if="item.ban_end.length > 0" v-for="end in item.ban_end" :src="`/end${end}.png`" alt="img"
                    width="80" />
            </div>
            <div class="col_part">
                <p>最终得分</p>
                <p class="final">{{ item.ban_score }}</p>
            </div>
        </div>
    </div>
</template>