<template>
  <div class="multiselect">
    <div
      class="header"
      @click="toggleMultiselect"
      :class="{ open: isOpen }"
      v-click-outside="closeMultiselect"
    >
      <ul class="header__list">
        <li
          class="header__item"
          v-for="(selected, index) in header"
          :key="index"
        >
          {{ selected }}
          <button class="header__close" @click.stop="deleteItem(selected)">
            <svg width="20" height="20" viewBox="0 0 20 20">
              <path
                d="M10.0006 8.82178L14.1256 4.69678L15.3039 5.87511L11.1789 10.0001L15.3039 14.1251L14.1256 15.3034L10.0006 11.1784L5.8756 15.3034L4.69727 14.1251L8.82227 10.0001L4.69727 5.87511L5.8756 4.69678L10.0006 8.82178Z"
              ></path>
            </svg>
          </button>
        </li>
      </ul>
      <svg class="header__icon" width="15" height="9" viewBox="0 0 15 8.53">
        <path
          d="M10,14.26A1,1,0,0,1,9.3,14L2.79,7.44A1,1,0,0,1,4.2,6L10,11.85,15.8,6a1,1,0,1,1,1.41,1.41L10.7,14A1,1,0,0,1,10,14.26Z"
          transform="translate(-2.5 -5.74)"
        ></path>
      </svg>
      <input
        type="search"
        class="search"
        placeholder="Choose artifact"
        ref="searchField"
        v-model="searchMatch"
        @input="getSearchMatch"
      />
    </div>
    <ul class="multiselect__list">
      <li
        class="multiselect__item"
        v-for="(item, i) in filteredList"
        :key="i"
        @click="selectItem(item)"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "VMultiselect",
  props: {
    list: {
      type: Array,
      default: [" "],
    },
    header: {
      type: Array,
      default: [],
    },
  },

  data: () => ({
    isOpen: false,
    searchMatch: "",
    filteredList: [],
  }),

  created() {
    this.filteredList = this.list;
  },

  // Я думаю, я сильно намудрил с поиском
  // чувствую, это как-то короче можно сделать...
  computed: {
    getSearchMatch() {
      this.filteredList = this.list.filter((el) => {
        return el.toLowerCase().includes(this.searchMatch);
      });
    },
  },

  methods: {
    toggleMultiselect() {
      this.isOpen = !this.isOpen;
      this.$refs.searchField.focus();
    },
    closeMultiselect() {
      this.isOpen = false;
    },
    selectItem(item) {
      this.$emit("select-item", item);
      this.searchMatch = "";
      this.$nextTick(() => {
        this.filteredList = this.list;
      });
    },
    deleteItem(item) {
      this.$emit("delete-item", item);
      this.$nextTick(() => {
        this.filteredList = this.list;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  width: 100%;
  padding: 8px 48px 8px 32px;
  background-color: #fff;
  border-radius: 8px;
  cursor: pointer;
  user-select: none;
  overflow: hidden;
  box-shadow: 0 0 16px rgba(10, 10, 10, 0.1);

  &__list {
    display: flex;
    align-items: center;
    gap: 6px 8px;
    flex-wrap: wrap;
    margin-bottom: 4px;
  }

  &__item {
    position: relative;
    flex-shrink: 0;

    padding: 6px 34px 6px 12px;
    border-radius: 4px;
    font-size: 14px;

    color: #fff;
    background-color: #c12d2d;
    transition: all 0.2s ease;
  }

  &__close {
    width: 26px;
    height: 26px;
    background-color: #b52323;
    transition: all 0.2s ease;
    cursor: pointer;

    display: flex;
    align-items: center;
    justify-content: center;

    position: absolute;
    top: 4px;
    right: 4px;
    border-radius: 4px;

    &:hover {
      background-color: #a71919;
      transition: all 0.2s ease;
    }

    & svg {
      display: block;
      fill: #fff;
    }
  }

  &__icon {
    fill: #565656;
    transition: all 0.2s ease;

    position: absolute;
    top: 22px;
    right: 22px;
    z-index: 10;
  }
}

.search {
  width: 100%;
  height: 38px;
  outline: none;

  font-family: inherit;
  font-weight: inherit;
  font-size: inherit;
  color: #565656;
  appearance: none;

  &::-webkit-search-decoration,
  &::-webkit-search-cancel-button,
  &::-webkit-search-results-button,
  &::-webkit-search-results-decoration {
    -webkit-appearance: none;
  }

  &::placeholder {
    color: #cbcbcb;
  }
}

.multiselect {
  position: relative;

  &__list {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    z-index: 10;

    width: 100%;
    border-bottom-left-radius: 6px;
    border-bottom-right-radius: 6px;
    overflow: hidden;
  }

  &__item {
    cursor: pointer;
    padding: 16px 32px;
    color: #565656;
    background-color: #fff;
    border-top: 1px solid #e9e6e6;
    transition: all 0.2s ease;

    &:hover {
      color: #fff;
      background-color: #c12d2d;
      transition: all 0.2s ease;
    }
  }
}

.header.open {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
  cursor: pointer;
  user-select: none;
  overflow: hidden;
  box-shadow: 0 0 16px rgba(10, 10, 10, 0.1);

  & + .multiselect__list {
    display: block;
  }

  & .header__icon {
    transform: rotate(180deg);
    fill: #c12d2d;
    transition: all 0.2s ease;
  }
}
</style>
