<template>
  <ul class="select" @click="openDropdown" :class="{ open: isOpen }">
    <li class="select__header">
      <span class="select__current">{{ header }}</span>
      <svg class="select__icon" width="15" height="9" viewBox="0 0 15 8.53">
        <path
          d="M10,14.26A1,1,0,0,1,9.3,14L2.79,7.44A1,1,0,0,1,4.2,6L10,11.85,15.8,6a1,1,0,1,1,1.41,1.41L10.7,14A1,1,0,0,1,10,14.26Z"
          transform="translate(-2.5 -5.74)"
        ></path>
      </svg>
    </li>
    <li
      class="select__item"
      v-for="(item, i) in list"
      :key="i"
      @click="$emit('change-header', item)"
    >
      {{ item.content }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "VDropdown",
  props: {
    list: {
      type: Array,
      default: () => [],
    },
    header: {
      type: String,
      default: "Choose something",
    },
  },

  data: () => ({
    isOpen: false,
  }),

  methods: {
    openDropdown() {
      this.isOpen = !this.isOpen;
    },
    closeDropdown() {
      this.isOpen = false;
    },
  },
};
</script>

<style scoped>
.select {
  width: 100%;
  max-height: 54px;
  background-color: #fff;
  border-radius: 8px;
  transition: all 0.2s ease;
  cursor: pointer;
  user-select: none;
  overflow: hidden;
  box-sizing: content-box;
  box-shadow: 0 0 16px rgba(10, 10, 10, 0.1);
}

.select.open {
  max-height: 100%;
}

.select__header {
  padding: 16px 32px;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.select__current {
  color: #565656;
  transition: all 0.2s ease;
}

.select__header:hover .select__current,
.select.open .select__current {
  color: #c12d2d;
  transition: all 0.2s ease;
}

.select__icon {
  fill: #565656;
  transition: all 0.2s ease;
}

.select.open .select__icon {
  transform: rotate(180deg);
}

.select__header:hover .select__icon,
.select.open .select__icon {
  fill: #c12d2d;
  transition: all 0.2s ease;
}

.select__item {
  padding: 16px 32px;
  color: #565656;
  background-color: #fff;
  border-top: 1px solid #e9e6e6;
  transition: all 0.2s ease;
}

.select__item:hover {
  color: #fff;
  background-color: #c12d2d;
  transition: all 0.2s ease;
}
</style>
