<template>
    <div class="container">
        <div v-if="score" v-for="item in score" class="team">
            <div class="name_score">
                <h2>队名: {{ item.name }}</h2>
                <h2>总分：{{ item.normal_score + item.speed_score + item.ban_score }}</h2>
            </div>
            <div class="detail">
                <div>
                    <h3>普通赛道</h3>
                    <p><span class="item">讲述者：</span>{{ item.normal_player }}</p>
                    <p><span class="item">开局主力：</span>{{ item.normal_startOperator }}</p>
                    <p><span class="item">开局分队：</span>{{ item.normal_startTeam }}</p>
                    <p><span class="item">完成结局：</span>{{ item.normal_end }}</p>
                    <p><span class="item">结算分：</span>{{ item.normal_settlement }}</p>
                    <p><span class="item">额外分：</span>{{ item.normal_extra }}</p>
                    <p><span class="item">普通赛道得分：</span>{{ item.normal_score }}</p>
                </div>
                <div>
                    <h3>竞速赛道</h3>
                    <p><span class="item">讲述者：</span>{{ item.speed_player }}</p>
                    <p><span class="item">开局主力：</span>{{ item.speed_startOperator }}</p>
                    <p><span class="item">开局分队：</span>{{ item.speed_startTeam }}</p>
                    <p><span class="item">完成结局：</span>{{ item.speed_end }}</p>
                    <p><span class="item">结算分：</span>{{ item.speed_settlement }}</p>
                    <p><span class="item">时间：</span>{{ item.speed_time }}</p>
                    <p><span class="item">竞速赛道得分：</span>{{ item.speed_score }}</p>
                </div>
                <div>
                    <h3>自限赛道</h3>
                    <p><span class="item">讲述者：</span>{{ item.ban_player }}</p>
                    <p><span class="item">开局主力：</span>{{ item.ban_startOperator }}</p>
                    <p><span class="item">开局分队：</span>{{ item.ban_startTeam }}</p>
                    <p><span class="item">完成结局：</span>{{ item.ban_end }}</p>
                    <p><span class="item">结算分数：</span>{{ item.ban_settlement }}</p>
                    <p><span class="item">额外分数：</span>{{ item.ban_extra }}</p>
                    <p><span class="item">自限赛道得分：</span>{{ item.ban_score }}</p>
                </div>
            </div>
        </div>
        <p v-else>加载中...</p>
    </div>
</template>

<style>
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

.team h2 {
    font-family: 'my-fztys';
    text-align: center;
}

.item {
    font-family: 'my-hwfs';
    font-weight: 700;
    font-size: 1rem;
}

.detail {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    gap: 8rem;
}

.detail h3 {
    font-family: 'my-hwzs';
    text-align: center;
}
</style>
  
<script lang="ts">
import { defineComponent } from 'vue';

interface Team {
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
  