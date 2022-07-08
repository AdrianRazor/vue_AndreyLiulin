<template>
  <div class="task" :class="{ done }">
    <div class="task-info">
      <h3 class="task__title">{{ title }}</h3>
      <p class="task__desc">{{ description }}</p>
      <div class="tag" :class="tagStyle">{{ tag?.content }}</div>
    </div>
    <div class="btns">
      <button class="task__done" @click="handleCheck">
        <img src="@/assets/icons/check.svg" alt="check" />
      </button>
      <button class="task__done" @click="handleEdit">
        <img src="@/assets/icons/edit.svg" alt="edit" />
      </button>
      <button class="task__done" @click="handleRemove">
        <img src="@/assets/icons/close.svg" alt="remove" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppTask",
  props: {
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      default: "",
    },
    tag: {
      type: Object,
      default: () => {},
    },
    done: {
      type: Boolean,
      default: false,
    },
  },

  computed: {
    tagStyle() {
      let className = "";

      switch (this.tag.id) {
        case 0:
          className = "work";
          break;
        case 1:
          className = "personal";
          break;
        case 2:
          className = "study";
          break;
        case 3:
          className = "sport";
          break;
        case 4:
          className = "leisure";
          break;
      }

      return className;
    },
  },

  methods: {
    handleRemove() {
      this.$emit("remove-task");
    },
    handleCheck() {
      this.$emit("check-task");
    },
    handleEdit() {
      this.$emit("edit-task");
    },
  },
};
</script>

<style>
.done {
  opacity: 0.3;
}
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  max-width: 100%;
  border-bottom: 1px solid #2f4858;
}
.task:hover:not(.done) {
  background-color: #2f485811;
}
.task__title {
  font-family: "Rubik", serif;
  font-style: normal;
  font-size: 24px;
  font-weight: 600;
}
.task__desc {
  font-family: "Rubik", serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
}
.task__done {
  height: 30px;
  width: 30px;
  border: none;
  background-color: unset;
}

.task__done img {
  width: inherit;
  height: inherit;
}

.task__done:hover {
  cursor: pointer;
  border-radius: 4px;
  background-color: #9ee493bb;
}

.task-info .tag {
  font-family: "Rubik", serif;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  border-radius: 10px;
  padding: 5px;
  display: inline-block;
  width: 75px;
  text-align: center;
  color: #fff;
}

.btns {
  display: flex;
  align-items: center;
}

.work {
  background-color: #19b994;
  border-color: #16836a;
}

.personal {
  background-color: #c8238e;
  border-color: #85207d;
}

.study {
  background-color: #979ddf;
  border-color: #462da9;
}

.sport {
  background-color: #19b994;
  border-color: #16836a;
}

.leisure {
  background-color: #19b994;
  border-color: #16836a;
}
</style>
