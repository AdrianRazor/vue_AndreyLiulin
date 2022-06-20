<template>
  <div class="progress">
    <div class="progress__bar" :style="widthStyle"></div>
  </div>
</template>

<script>
export default {
  name: "AppProgress",
  props: {
    width: {
      type: Number,
      required: true,
    },
  },

  computed: {
    widthStyle() {
      return {
        width: this.width + "%",
      };
    },
  },
};
</script>

<style scoped>
.progress {
  width: 100%;
  height: 20px;
  border-radius: 20px;
  background-color: #7e1826;
  overflow: hidden;
  margin-bottom: 40px;
}

.progress__bar {
  height: 20px;
  border-radius: 20px;
  background-color: #bf263b;
  box-shadow: 2px 0 10px #38030b;
  transition: all 0.3s ease;
}
</style>
