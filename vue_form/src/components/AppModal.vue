<template>
  <div
    class="info"
    tabindex="-1"
    @click.self="$emit('close-modal')"
    @keydown.esc="$emit('close-modal')"
  >
    <transition name="openmodal" appear>
      <div class="info__window">
        <h2 class="info__title">Infrormation</h2>
        <ul class="info__list">
          <li class="info__item" v-for="(item, i) in items" :key="i">
            <span class="info__label">{{ item.name }}</span>
            <span class="info__text">{{ item.value }}</span>
          </li>
        </ul>

        <button
          class="form__btn-send"
          type="button"
          @click="$emit('close-modal')"
        >
          okay
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "AppModal",
  props: {
    items: {
      type: Array,
      required: true,
    },
    name: {
      type: String,
      default: " ",
    },
    value: {
      type: String,
      default: " ",
    },
  },

  mounted() {
    this.$el.focus();
  },
};
</script>

<style scoped>
.info {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.4);

  position: absolute;
  top: 0;
  left: 0;
  z-index: 10;
}

.info__window {
  max-width: 500px;
  width: 100%;
  background-color: #1d1d28;
  padding: 40px;
  border-radius: 24px;

  display: flex;
  flex-direction: column;
  align-items: center;
}
.info__list {
  width: 100%;
  list-style: none;
}
.info__title {
  font-size: 26px;
  color: #fff;
  text-transform: uppercase;
  text-align: center;
  margin-bottom: 15px;
}

.info__item {
  font-family: inherit;
  font-size: 16px;
  color: #aaa;
  outline: none;

  width: 100%;
  padding: 10px 18px;
  background-color: transparent;
  border: 1px solid #bf263b;
  border-radius: 24px;
}

.info__item:not(:last-child) {
  margin-bottom: 15px;
}

.info__label {
  position: relative;
  display: inline-block;
  margin-right: 50px;
}

.info__label::after {
  content: "";
  width: 2px;
  height: 25px;
  background-color: #444;

  position: absolute;
  top: 0;
  right: -25px;
}

.info__text,
.info__guest {
  color: #fff;
}

.info__guests {
  display: flex;
}

.openmodal-enter-from {
  opacity: 0;
  transform: translateY(-30px);
}
.openmodal-enter-to {
  opacity: 1;
  transform: translateY(0px);
  transition: opacity 0.3s ease, transform 0.5s ease;
}
</style>
