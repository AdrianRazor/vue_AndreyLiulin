<template>
  <div
    class="modal"
    tabindex="-1"
    @click.self="$emit('close-modal')"
    @keydown.esc="$emit('close-modal')"
  >
    <div class="modal__window">
      <div class="modal__content">
        <slot name="header"></slot>
        <slot></slot>
        <slot name="footer"></slot>
      </div>
      <slot name="aside"></slot>
      <button id="close" @click="$emit('close-modal')">
        <svg viewBox="0 0 20 20">
          <path
            d="M10.0006 8.82178L14.1256 4.69678L15.3039 5.87511L11.1789 10.0001L15.3039 14.1251L14.1256 15.3034L10.0006 11.1784L5.8756 15.3034L4.69727 14.1251L8.82227 10.0001L4.69727 5.87511L5.8756 4.69678L10.0006 8.82178Z"
          ></path>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "VModal",

  mounted() {
    this.$el.focus();
  },
};
</script>

<style>
.modal {
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);

  display: flex;
  justify-content: center;
  align-items: center;

  position: absolute;
  top: 0;
  left: 0;
}

.modal__window {
  position: relative;
  max-width: 800px;
  width: 100%;
  padding: 24px 40px;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);

  background-image: url(@/assets/img/bg-modal.jpg);
  background-repeat: no-repeat;
  background-position: center top;
  background-size: cover;

  display: flex;
  align-items: center;
  justify-content: space-between;
}

#close {
  width: 32px;
  height: 32px;
  background-color: transparent;
  fill: #cdcdcd;
  cursor: pointer;
  transition: all 0.2s ease;

  position: absolute;
  top: 32px;
  right: 32px;
  z-index: 10;
}

#close:hover {
  fill: #fff;
  transition: all 0.2s ease;
}

/* Header */
.modal__stat {
  display: flex;
  align-items: center;
}

.modal__stat-icon {
  width: 32px;
  height: 32px;
}

.modal__stat-title {
  margin-left: 6px;
  font-size: 24px;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: #fff;
}

.modal__title {
  margin-top: 12px;
  font-size: 64px;
  line-height: 1;
  text-transform: uppercase;
  color: #fff;
}

.modal__subtitle {
  margin-top: 8px;
  font-size: 18px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #a5e0f3;
}

/* Body */
.modal__text {
  margin-top: 32px;
  font-size: 16px;
  color: #fff;
}

.modal__link {
  display: inline-block;
  margin-top: 8px;
  border-bottom: 1px solid #959595;
  font-size: 14px;
  color: #959595;
  text-decoration: none;
}

.modal__link:hover {
  color: #fff;
  border-color: #fff;
}

/* Footer */
.modal__footer {
  margin-top: 32px;
  display: flex;
}

.modal__block:not(:first-of-type) {
  margin-left: 32px;
}

.modal__headline {
  font-size: 16px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #959595;
}

.modal__type {
  margin-top: 4px;
  display: flex;
  align-items: center;
}

.modal__type-icon {
  width: 18px;
  height: 18px;
}

.modal__type-text {
  font-size: 14px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #fff;
  margin-left: 8px;
}

.modal__complexity {
  margin-top: 8px;
  margin-left: 4px;
  display: flex;
  align-items: center;
  gap: 0 12px;
}

.modal__rhombus {
  width: 12px;
  height: 12px;
  border: 1px solid #fff;
  transform: rotate(45deg);
}

.modal__rhombus.fill {
  background-color: #fff;
}

/* Aside */
.modal__img {
  max-width: 400px;
  width: 100%;
}
</style>
