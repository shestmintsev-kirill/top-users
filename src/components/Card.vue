<template>
  <CardModal
    v-if="showModal"
    :card="card"
    :cards="cards"
    :index="index"
    :sortDescending="sortDescending"
    @closeModal="showModal = false"
  />
  <ul>
    <li @click="showModal = true" class="card">
      <div class="card-wrapper">
        <img
          v-if="!sortDescending"
          :class="{
            gold: index === 0,
            silver: index === 1,
            bronze: index === 2,
          }"
          class="card-avatar"
          :src="`${card.avatar}`"
          alt="avatar"
        />
        <img
          v-else
          :class="{
            gold: index === cards.length - 1,
            silver: index === cards.length - 2,
            bronze: index === cards.length - 3,
          }"
          class="card-avatar"
          :src="`${card.avatar}`"
          alt="avatar"
        />
        <div class="card-name">
          <p>Пользователь:</p>
          <p>{{ card.name }}</p>
        </div>
      </div>
      <div class="card-ranking">
        <img src="../assets/star.png" alt="star-ranking" />
        <span class="rating">{{ card.rating }}</span>
      </div>
    </li>
  </ul>
</template>

<script>
import CardModal from "./CardModal.vue";
export default {
  components: { CardModal },
  name: "Card",
  props: {
    card: {
      type: Object,
    },
    index: {
      type: Number,
    },
    sortDescending: {
      type: Boolean,
    },
    cards: {
      type: Array,
    },
  },
  data: () => ({
    showModal: false,
  }),
};
</script>

<style scoped lang="scss">
@import "../assets/style.scss";

.card {
  height: 88px;
  padding: 10px;
  display: flex;
  border-radius: 10px;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s;
  cursor: pointer;

  &:hover {
    background: rgba(0, 0, 0, 0.07);
  }

  &-wrapper {
    display: flex;
    align-items: center;
  }

  &-avatar {
    border-radius: 50%;
    width: 60px;
    height: 60px;
    margin-right: 24px;
  }

  &-name {
    line-height: 19px;
  }

  &-ranking {
    display: flex;
    align-items: center;

    .rating {
      margin-left: 7px;
      font-size: 18px;
    }
  }
}

.gold {
  border: 4px solid #fdd835;
}

.silver {
  border: 4px solid #90a4ae;
}

.bronze {
  border: 4px solid #795548;
}
</style>
