<template>
  <div @click.self="$emit('closeModal')" class="after-mask">
    <div class="after-wrapper">
      <div class="after-container">
        <div class="after-container-header">
          <p>Профиль пользователя:</p>
          <img
            @click.self="$emit('closeModal')"
            class="exit"
            src="../assets/exit.png"
            alt="exit-modal"
          />
        </div>
        <div class="after-container-card">
          <img class="avatar" :src="`${card.avatar}`" alt="user-avatar" />
          <div class="after-container-card-info">
            <ul>
              <li class="fz18">Имя:</li>
              <li>{{ card.name }}</li>
              <li class="fz18">Баллы:</li>
              <li>{{ card.rating }}</li>
              <li class="fz18">Позиция в рейтинге:</li>
              <li v-if="!sortDescending">{{ index + 1 }}</li>
              <li v-else>{{ cards.length - index }}</li>
            </ul>
          </div>
        </div>
        <div class="after-container-card-footer">
          <p>О себе:</p>
          <p>{{ card.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardModal",
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
};
</script>

<style scoped lang="scss">
@import "../assets/style.scss";

.after-mask {
  position: fixed;
  z-index: 2;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: opacity 0.3s ease;
}

.after-container {
  width: 480px;
  height: auto;
  padding: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(255, 255, 255);
  transition: all 0.3s ease;
  animation: opacity 0.3s linear;

  &-header {
    width: 100%;
    display: flex;
    justify-content: space-between;
    margin-bottom: 26px;
    font-size: 24px;

    .exit {
      height: 16px;
      width: 16px;
      cursor: pointer;
    }
  }

  &-card {
    width: 100%;
    display: flex;
    align-items: center;
    margin-bottom: 17px;

    .avatar {
      border-radius: 50%;
      width: 130px;
      height: 130px;
    }

    &-info {
      margin-left: 37px;
      line-height: 18px;
    }

    &-footer {
      width: 100%;
      font-size: 18px;
    }
  }
}

.fz18 {
  font-size: 18px;
}
</style>
