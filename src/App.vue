<template>
  <div class="pg">
    <div class="pg__prize-list">
      <div 
        v-for="item in prizes" 
        :key="item.id" 
        class="pg__prize-item"
        @click="get(item)">
        <div class="pg__prize-item-wrapper">
          <div
            class="pg__prize-item-img"
            :style="{ backgroundImage: `url('${item.imgUrl}')` }">
            <div class="pg__prize-item-name">
              {{ item.name }} {{ item.count }}
            </div>
          </div>
          <div class="pg__prize-item-min">积分累计达到{{ item.min }}</div>
          <div :class="['pg__prize-item-btn', item.has ? 'pg__prize-item-btn--has' : '']">{{ item.has ? '已领取' : '领取' }}</div>
        </div>
      </div>
    </div>
    <div class="pg__user-info">
      <div class="pg__user-info-left">当前积分{{ userInfo.score }}</div>
      <div class="pg__user-info-right">
        <div>登录游戏</div>
        <div>登录游戏</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      userInfo: {
        score: 20,
      },
      // 模拟奖品数据
      prizes: new Array(3).fill("").map((item, idx) => {
        return {
          id: idx,
          // 奖品
          name: "金币", 
          // 数量
          count: 1000, 
          // 奖品图片
          imgUrl: "https://png.pngtree.com/background/20210716/original/pngtree-pink-yellow-clouds-cute-baby-background-picture-image_1342434.jpg", 
          // 领取要求
          min: 10 * (idx + 1), 
          // 是否领取
          has: idx === 0 ? true : false,
        };
      }),
    };
  },
  methods: {
    get(item) {
      // 已经领取
      if (item.has) return
      // 可以领取
      if (this.userInfo.score >= item.min) {
        alert("领取成功")
        item.has = true
        return
      }
      // 积分不够
      alert("积分不够")
    }
  }
};
</script>

<style lang="less">
.pg {
  font-size: 14px;
}
.pg__prize-list {
  display: flex;
}

.pg__prize-item {
  flex-shrink: 0;
  width: 33%;
}
.pg__prize-item-wrapper {
  
}
.pg__prize-item-img {
  width: 88px;
  height: 88px;
  margin: auto;
  background: red;
  position: relative;
  margin-bottom: 8px;
}
.pg__prize-item-name {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, .1);
  text-align: center;
}
.pg__prize-item-btn {
  background: yellow;
  &--has {
    background: gray;
  }
}

.pg__user-info {
  display: flex;
  align-items: center;
  margin: 12px;
  background: green;
  padding: 12px;
  &-left {
    padding-right: 12px
  }
}
</style>
