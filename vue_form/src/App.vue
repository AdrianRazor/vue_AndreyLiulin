<template>
  <div class="form">
    <form class="form__wrapper">
      <app-progress :width="calculateWidth"></app-progress>
      <app-field
        v-for="(field, i) in info"
        :key="i"
        :value="field.value"
        :pattern="field.pattern"
        :valid="field.valid"
        :activated="field.activated"
        @on-input="handleInput($event, i)"
      ></app-field>
      <button class="form__btn-send" :disabled="!formReady">Send Data</button>
    </form>
  </div>
</template>

<script>
import AppField from "./components/AppField.vue";
import AppProgress from "./components/AppProgress.vue";

export default {
  components: {
    AppField,
    AppProgress,
  },
  created() {
    return this.info.forEach((element) => {
      element.valid = false;
      element.activated = false;
    });
  },

  data: () => ({
    info: [
      {
        name: "Name",
        value: "",
        pattern: /^[a-zA-Z ]{2,30}$/,
      },
      {
        name: "Phone",
        value: "",
        pattern: /^[0-9]{7,14}$/,
      },
      {
        name: "Email",
        value: "",
        pattern: /.+/,
      },
      {
        name: "Additional info 1",
        value: "",
        pattern: /.+/,
      },
      {
        name: "Additional info 2",
        value: "",
        pattern: /.+/,
      },
    ],
  }),

  computed: {
    validInputs() {
      return this.info.reduce((total, item) => {
        return total + (item.valid ? 1 : 0);
      }, 0);
    },
    formReady() {
      return this.validInputs === this.info.length;
    },
    calculateWidth() {
      return (this.validInputs / this.info.length) * 100;
    },
  },

  methods: {
    handleInput(value, i) {
      const field = this.info[i];
      field.value = value;
      field.activated = true;
      field.valid = field.pattern.test(value);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap");

* {
  margin: 0;
  padding: 0;
  border: 0;
  box-sizing: border-box;
}

body {
  width: 100%;
  height: 100%;
  background-color: #1d1d28;
  font-family: "Poppins", sans-serif;
  font-style: normal;
  font-weight: 400;
}

.form {
  width: 100%;
  display: flex;
  justify-content: center;
}

.form__wrapper {
  max-width: 500px;
  width: 100%;
  padding-top: 100px;
}

.form__btn-send {
  width: 50%;
  padding: 10px 18px;
  background-color: #bf263b;
  border-radius: 24px;
  cursor: pointer;
  margin-top: 40px;

  font-family: inherit;
  font-weight: 600;
  font-size: 16px;
  color: #fff;
  text-transform: uppercase;

  transition: all 0.3s ease;
}

.form__btn-send:hover {
  box-shadow: 0 0 10px #bf263b;
  transition: all 0.2s ease;
}

.form__btn-send:disabled {
  pointer-events: none;
  background-color: #292935;
  color: #666;
  transition: all 0.2s ease;
}
</style>
