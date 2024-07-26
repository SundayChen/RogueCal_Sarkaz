<template>
  <div class="rules">
    <h2>可汗杯 萨卡兹肉鸽赛季 赛事规则</h2>
    <div class="ruleItem">
      <p>
        <span class="order">1. </span>
        本次比赛由
        <a href="https://space.bilibili.com/122574257">你有五根棒棒糖嘛w</a>
        策划，旨在为群友提供一个展示自己技术的平台
      </p>
      <p>
        <span class="order">2. </span>
        所有参赛选手需使用 <a href="https://prts.wiki/w/%E8%90%A8%E5%8D%A1%E5%85%B9%E7%9A%84%E6%97%A0%E7%BB%88%E5%A5%87%E8%AF%AD">
          萨卡兹的无终奇语
        </a>
        集成战略主题作为比赛场景，且必须使用15级难度开局
      </p>
      <p>
        <span class="order">3. </span>
        比赛赛程暂定于8月9-12号（活动策划有权更改赛程），具体时间将在群内公布
      </p>
      <p>
        <span class="order">4. </span>
        比赛将全程使用腾讯会议进行直播，并由活动策划与部分选手进行解说
      </p>
      <p>
        <span class="order">5. </span>
        比赛赛制为团队赛，参赛选手将分为两队。每个队伍需要选出两名选手参加速通赛道和自限赛道，其余选手均参与普通赛道。
      </p>
      <p class="ruleMultiRow">
        普通赛道取每个队伍的最高分，加上各队速通和自限赛道的分数为团队总分，总分高的队伍获胜
      </p>
    </div>

    <h2>个人积分细则</h2>
    <div class="personalScore">
      <div class="psItem">
        <h3>普通赛道</h3>
        <p>
          <span class="order">1. </span>
          临时招募六星+50分，五星+20分，四星+10分
        </p>
        <p>
          <span class="order">2. </span>
          三层异格boss+50分，完成二结局+100分，完成三结局+200分，同时完成二三结局额外+100分
        </p>
        <p>
          <span class="order">3. </span>
          取队伍中最高分的选手的分数作为该队伍的普通赛道分
        </p>
      </div>

      <div class="psItem">
        <h3>速通赛道</h3>
        <p>
          <span class="order">1. </span>
          完成任意结局：满分6000分，结算时间每秒-2分，最低2400分
        </p>
        <p>
          <span class="order">2. </span>
          未完成结局：以结算分为得分，最高取2400分
        </p>
        <p>
          <span class="order">3. </span>
          每个选手有两次机会，取较高者作为该队伍的速通赛道分
        </p>
      </div>

      <div class="psItem">
        <h3>自限赛道</h3>
        <p>
          <span class="order">1. </span>
          以规则制定时的数据为准，选手每禁用一个各职业使用率最高的干员+50分
        </p>
        <p>
          <span class="order">2. </span>
          不使用蓝图测绘分队+100分
        </p>
        <p>
          <span class="order">3. </span>
          临时招募与BOSS得分与普通赛道相同
        </p>
        <p>
          <span class="order">4. </span>
          每个选手在第三层第一个节点之前有一次重开的机会，不使用重开机会+50分
        </p>
        <p>
          <span class="order">5. </span>
          选手最终得分*1.1倍（向上取整）作为该队伍的自限赛道得分
        </p>
      </div>
    </div>
  </div>
</template>

<style>
.order {
  font-weight: 700;
  font-family: 'Times New Roman', Times, serif;
  font-size: 1.2rem;
}

.rules {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.ruleMultiRow {
  text-indent: 1.1em;
}

.rulesItem {
  align-items: flex-start;
  text-align: left;
  gap: 5px;
}

.rules h2 {
  font-size: 1.5rem;
  font-weight: 600;
  font-family: '华文中宋';
  margin-top: 1rem;
}

.rules p {
  font-size: 1rem;
}

.personalScore {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: center;
}

.psItem {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  text-align: left;
  gap: 5px;
  margin-left: 30px;
  margin-right: 30px;
}

.psItem h3 {
  font-family: '华文中宋';
}
</style>
