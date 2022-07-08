<template>
  <div class="wrapper">
    <div>
      <p>
        Количество задач: <span>{{ localData.length }}</span>
      </p>
      <p>
        Количество выполненных задач: <span>{{ tasksDoneCount }}</span>
      </p>
    </div>
    <button @click="toggleModal">Add New Task</button>
    <app-task
      v-for="(item, i) in localData"
      :key="item.title + i"
      :title="item.title"
      :description="item.description"
      :tag="item.tag"
      :done="item.done"
      @remove-task="removeTask(i)"
      @check-task="taskChangeStatus(i)"
      @edit-task="editTask(i)"
    ></app-task>
    <app-modal v-if="isModalOpen" @close-modal="isModalOpen = false">
      <input
        ref="input"
        placeholder="Новая задача"
        type="text"
        v-model="newData.title"
      />
      <textarea
        placeholder="Описание"
        type="text"
        v-model="newData.description"
      ></textarea>
      <app-dropdown
        :list="categories"
        :header="newData.tag?.content"
        @change-header="changeCategory"
      ></app-dropdown>
      <button @click="modalBtnAction">{{ modalBtnContent }}</button>
    </app-modal>
  </div>
</template>

<script>
import AppTask from "@/components/AppTask.vue";
import AppModal from "@/components/AppModal.vue";
import AppDropdown from "@/components/AppDropdown.vue";

export default {
  name: "App",
  components: {
    AppTask,
    AppModal,
    AppDropdown,
  },

  data: () => ({
    defaultData: [
      {
        title: "Запланировать Урок",
        description: "Подготовить шаблон компонента",
        tag: {
          id: 0,
          content: "Работа",
        },
        done: false,
      },
      {
        title: "Встретиться с девушкой",
        description: "Позвонить и договориться о встрече",
        tag: {
          id: 1,
          content: "Личное",
        },
        done: false,
      },
      {
        title: "Прочитать документацию по JS",
        description: "js",
        tag: {
          id: 2,
          content: "Учеба",
        },
        done: false,
      },
      {
        title: "Тренировка",
        description: "Сходить на тренировку",
        tag: {
          id: 3,
          content: "Спорт",
        },
        done: false,
      },
      {
        title: "Сыграть с другом",
        description: "Предложить сыграть в какую-то стратежку",
        tag: {
          id: 4,
          content: "Досуг",
        },
        done: false,
      },
    ],
    isModalOpen: false,
    localData: null,
    newData: {
      title: "",
      description: "",
      tag: {},
      done: false,
    },
    editMode: false,
    activeTask: null,
  }),

  created() {
    this.newData.tag = this.categories[0];
    this.localData = localStorage.getItem("localData")
      ? JSON.parse(localStorage.getItem("localData"))
      : this.defaultData;
  },

  computed: {
    categories() {
      const arr = [];

      this.localData?.forEach((item) => {
        if (arr.findIndex((obj) => obj.id === item.tag.id) === -1) {
          arr.push(item.tag);
        }
      });

      return arr;
    },
    tasksDoneCount() {
      return this.localData.reduce((acc, item) => acc + (item.done ? 1 : 0), 0);
    },
    modalBtnContent() {
      return this.editMode ? "Save changes" : "Add";
    },
    modalBtnAction() {
      return this.editMode ? this.saveEditedTask : this.addTask;
    },
  },
  watch: {
    "localData.length"() {
      this.saveData();
    },
  },
  methods: {
    toggleModal() {
      this.isModalOpen = !this.isModalOpen;

      if (!this.isModalOpen) {
        this.newData = {
          title: "",
          description: "",
          tag: {},
          done: false,
        };
        this.editMode = false;
      }
    },
    saveData() {
      localStorage.setItem("localData", JSON.stringify(this.localData));
    },
    addTask() {
      const obj = Object.assign({}, this.newData);
      this.localData.push(obj);
      this.toggleModal();
    },
    editTask(i) {
      this.activeTask = i;
      this.editMode = true;
      this.toggleModal();
      const obj = Object.assign({}, this.localData[i]);
      this.newData = obj;
    },
    saveEditedTask() {
      this.localData[this.activeTask] = { ...this.newData };
      this.toggleModal();
    },
    changeCategory(obj) {
      this.newData.tag = obj;
    },
    removeTask(i) {
      this.localData.splice(i, 1);
    },
    taskChangeStatus(i) {
      this.localData[i].done = !this.localData[i].done;
    },
  },
};
</script>

<style>
.wrapper {
  padding: 100px 300px;
}
</style>
