<script setup lang='ts'>
import { ref } from 'vue';
import Ban from '../components/scoreBoard/ban.vue';
import Normal from '../components/scoreBoard/normal.vue';
import Speed from '../components/scoreBoard/speed.vue';

const selected = ref<string[]>(['normal', 'normal']);
const tabs = ['normal', 'speed', 'ban'];
</script>

<template>
    <div class="container">
        <div v-if="score" v-for="(item, index) in score" class="team">
            <div class="name_score">
                <h1>队名: {{ item.name }}</h1>
                <h1>总分：{{ item.normal_score + item.speed_score + item.ban_score }}</h1>
            </div>
            <nav class="links">
                <a v-for="(tab, tabIndex) in tabs" :key="tabIndex" @click="selected[index] = tab"
                    :class="{ selected: selected[index] === tab }">
                    {{ tab == 'normal' ? '普通赛道' : tab == 'speed' ? '竞速赛道' : '速通赛道' }}
                </a>
            </nav>
            <div class="detail">
                <Normal v-if="selected[index] === 'normal'" :item="item" />
                <Speed v-else-if="selected[index] === 'speed'" :item="item" />
                <Ban v-else-if="selected[index] === 'ban'" :item="item" />
            </div>
        </div>
        <p v-else>加载中...</p>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-top: 2rem;
}

.name_score {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
}

.team {
    margin-bottom: 3em;
}

.team h1 {
    font-family: 'my-fztys';
    text-align: center;
    font-size: 2rem;
}

.links {
    display: flex;
    flex-direction: row;
    justify-content: center;
}

nav {
    width: 100%;
    font-size: 15px;
    text-align: center;
    margin-top: 0.5rem;
    margin-bottom: 0.7rem;
}

a {
    border: none;
    padding: 0 1rem;
    font-size: 1.2rem;
    cursor: pointer;
    font-family: 'my-hwzs';
    transition: color 0.3s ease, font-weight 0.3s ease;
}

a.hover {
    background-color: transparent;
}
a.selected {
    color: var(--color-text);
    font-weight: 700;
    pointer-events: none;
}
</style>
  
<script lang="ts">
import { defineComponent } from 'vue';

export interface Team {
    name: string;

    normal_player: string;
    normal_settlement: number;
    normal_extra: number;
    normal_score: number;
    normal_startOperator: string;
    normal_startTeam: string;
    normal_end: Number[];

    speed_player: string;
    speed_isFinish: boolean;
    speed_settlement: number;
    speed_time: string;
    speed_score: number;
    speed_startOperator: string;
    speed_startTeam: string;
    speed_end: Number[];

    ban_player: string;
    ban_settlement: number;
    ban_extra: number;
    ban_score: number;
    ban_startOperator: string;
    ban_startTeam: string;
    ban_end: Number[];
}

interface Score {
    teamScore: Team[]
}

export default defineComponent({
    data() {
        return {
            score: [] as Team[],
        };
    },
    methods: {
        async fetchData() {
            try {
                const response = await fetch('/score.json');
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                const json = await response.json() as Score;
                this.score = json.teamScore as Team[];
                this.calculateScores();
            } catch (error) {
                console.error('Error fetching the JSON file:', error);
            }
        },
        calculateScores() {
            for (const team of this.score) {
                team.normal_score = team.normal_settlement + team.normal_extra;

                if (team.speed_isFinish) {
                    const hours = parseInt(team.speed_time.split(':')[0]);
                    const minutes = parseInt(team.speed_time.split(':')[1]);
                    const seconds = parseInt(team.speed_time.split(':')[2]);
                    const teamSpeed = 6000 - (hours * 3600 + minutes * 60 + seconds) * 2;
                    team.speed_score = teamSpeed < 2400 ? 2400 : teamSpeed;
                } else
                    team.speed_score = team.speed_settlement > 2400 ? 2400 : team.speed_settlement;

                team.ban_score = Math.ceil((team.ban_settlement + team.ban_extra) * 1.1);
            }
        }
    },
    mounted() {
        this.fetchData();
    }
});
</script>
  