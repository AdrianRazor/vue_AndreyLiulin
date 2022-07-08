<template>
  <div class="form__item">
    <input
      type="text"
      class="form__input"
      :placeholder="placeholder"
      @input="$emit('on-input', $event.target.value)"
      required
    />
    <transition
      name="roll"
      v-if="activated"
      mode="out-in"
      appear
      appear-from-class="fade-enter-from"
      appear-to-class="fade-enter-to"
    >
      <img
        class="form__icon"
        src="../assets/img/valid.svg"
        alt="valid"
        v-if="valid"
      />
      <img
        class="form__icon"
        src="../assets/img/invalid.svg"
        alt="invalid"
        v-else
      />
    </transition>
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
    placeholder: {
      type: String,
      default: " ",
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
  width: 35px;
  height: 35px;
  margin-left: 15px;
}

/* Animation */
.fade-enter-from {
  opacity: 0;
  transform: translateX(20px);
}
.fade-enter-to {
  opacity: 1;
  transform: translateX(0px);
  transition: all 0.2s ease;
}

.roll-leave-from {
  transform: scaleX(1);
  transition: all 0.1s ease;
}
.roll-leave-to {
  transform: scaleX(0);
  transition: all 0.1s ease;
}
.roll-enter-from {
  transform: scaleX(0);
  transition: all 0.1s ease;
}
.roll-enter-to {
  transform: scaleX(1);
  transition: all 0.1s ease;
}
</style>
