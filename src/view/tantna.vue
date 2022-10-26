<template>
  <div class="tantan">
    <p style="text-align: center">POF</p>
    <div style="height: 300px">
      <Card
        ref="cardRef"
        @onDragMove="onCardDragMove"
        @onDragStop="onCardDragStop"
        @onThrowDone="onCardThrowDone"
        :cardWidth="300"
        :cardHeight="300"
        :throwTriggerDistance="100"
        dragDirection="horizontal"
        :hasShadow="true"
      >
        <template #firstCard>
          <div v-if="actionName === '喜欢'" class="maskLike">
            <img style="width: 50%; height: 50%" src="../static/like1.png" />
          </div>
          <div v-if="actionName === '不喜欢'" class="maskDislike">
            <img style="width: 50%; height: 50%" src="../static/dislike.png" />
          </div>
          <img
            v-if="cards[0]"
            :src="cards[0].image"
            style="width: 100%; height: 100%"
            mode="aspectFill"
          />
        </template>
        <template #secondCard>
          <img
            v-if="cards[1]"
            :src="cards[1].image"
            style="width: 100%; height: 100%"
            mode="aspectFill"
          />
        </template>
        <template #thirdCard>
          <img
            v-if="cards[2]"
            :src="cards[2].image"
            style="width: 100%; height: 100%"
            mode="aspectFill"
          />
        </template>
      </Card>
    </div>
    <img src="" alt="" />
    <!-- 描述 -->
    <div>
      <h2>David</h2>
      <div>
        <span>23,</span>
        <span>Model,</span>
        <span>175cm</span>
      </div>
    </div>
    <!-- 按钮 -->
    <div class="btn">
      <div @click="gun">
        <p>滚蛋</p>
      </div>

      <div @click="wc">
        <p>我草</p>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "../components/card.vue";
export default {
  components: {
    Card,
  },
  data() {
    return {
      hh: "",
      actionName: "",
      cards: [
        {
          image:
            "https://tva2.sinaimg.cn/large/0072Vf1pgy1foxli6nh8ij31hc0u0000.jpg",
        },
        {
          image:
            "https://tva3.sinaimg.cn/large/0072Vf1pgy1foxkfowh7rj31hc0u0ws9.jpg",
        },
        {
          image: "https://api.dujin.org/bing/1366.php",
        },
        {
          image: "https://www.dmoe.cc/random.php",
        },
        {
          image: "https://img.paulzzh.com/touhou/random",
        },

      ],
    };
  },
  methods: {
    onCardDragMove(obj) {
      console.log(obj);

      if (obj.left < -10) {
        this.actionName = "不喜欢";
      } else if (obj.left > 10) {
        this.actionName = "喜欢";
      } else {
        this.actionName = "";
      }
    },
    onCardDragStop() {
      this.actionName = "";
    },
    onCardThrowDone() {
      this.cards.splice(0, 1);
    },
    gun() {
      this.$refs.cardRef.makeCardThrowLeft();
      this.actionName = "不喜欢";
      setTimeout(() => {
        this.actionName = "";
      }, 1000);
      console.log();
    },
    wc() {
      this.$refs.cardRef.makeCardThrow();
      this.actionName = "喜欢";
      setTimeout(() => {
        this.actionName = "";
      }, 1000);
    },
  },
};
</script>

<style scoped>
.btn {
  margin-top: 30px;
  display: flex;
  justify-content: space-around;
}
.maskDislike,
.maskLike {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.maskDislike {
  background-color: rgba(0, 0, 0, 0.6);
}
.maskLike {
  background-color: rgba(233, 191, 182, 0.6);
}
.tantan {
  padding: 0 30px;
  box-sizing: border-box;
}
</style>
