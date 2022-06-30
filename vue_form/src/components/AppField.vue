<template>
  <div class="form__item">
    <input
      type="text"
      class="form__input"
      @input="$emit('on-input', $event.target.value)"
      required
    />
    <div class="form__icon" v-if="activated" :class="{ valid: valid }"></div>
  </div>
</template>

<script>
export default {
  name: "AppField",
  props: {
    valid: {
      type: Boolean,
      default: false,
    },
    activated: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.form__item {
  display: flex;
  align-items: center;
}

.form__item:not(:last-child) {
  margin-bottom: 20px;
}

.form__input {
  font-family: inherit;
  font-size: 16px;
  color: #fff;
  outline: none;

  width: 450px;
  padding: 10px 18px;
  background-color: transparent;
  border: 1px solid #bf263b;
  border-radius: 24px;
}

.form__input:focus {
  box-shadow: 0 0 6px #ff0022;
}

.form__icon {
  background-image: url(../assets/img/invalid.svg);
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  width: 35px;
  height: 35px;
  margin-left: 15px;
}

.form__icon.valid {
  background-image: url(../assets/img/valid.svg);
}
</style>
