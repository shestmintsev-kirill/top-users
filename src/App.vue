<template>
  <div class="section-outer">
    <div class="section-inner">
      <div class="content">
        <p class="content-title">Рейтинг пользователей:</p>
        <button @click="sortDescending = !sortDescending" class="content-btn">
          <img src="./assets/btn.png" alt="button-ranking" />
        </button>
      </div>
      <div class="content-cards">
        <Card
          v-for="(card, index) in cards"
          :key="card.id"
          :card="card"
          :index="index"
          :sortDescending="sortDescending"
          :cards="cards"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
export default {
  name: "App",
  components: { Card },
  data: () => ({
    cards: null,
    sortDescending: false,
  }),
  async mounted() {
    const f = await fetch(
      "https://my-json-server.typicode.com/Vespand/crmm-tasks/users"
    );
    const data = await f.json();
    this.cards = data.sort((prev, next) => {
      if (prev.rating > next.rating) return -1;
      if (prev.rating > next.rating) return 1;
    });
  },
  watch: {
    sortDescending() {
      if (this.sortDescending) {
        this.cards = this.cards.sort((prev, next) => {
          if (prev.rating < next.rating) return -1;
          if (prev.rating < next.rating) return 1;
        });
      } else {
        this.cards = this.cards.sort((prev, next) => {
          if (prev.rating > next.rating) return -1;
          if (prev.rating > next.rating) return 1;
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./assets/style.scss";

.section-outer {
  padding: 0 20px;
}

.section-inner {
  max-width: 600px;
  margin: 0 auto;
}

.content {
  display: flex;
  justify-content: space-between;
  margin-bottom: 23px;

  &-title {
    font-size: 24px;
    line-height: 34px;
  }

  &-btn {
    border-radius: 8px;
    border: 1px solid rgba(44, 62, 80, 0.67);
    outline: none;
    cursor: pointer;
    background: none;
    display: flex;
    align-items: center;
    transition: all 0.3s;

    &:hover {
      background-color: rgba(0, 0, 0, 0.07);
    }
  }
}
</style>
