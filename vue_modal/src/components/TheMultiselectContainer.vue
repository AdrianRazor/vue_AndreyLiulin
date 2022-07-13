<template>
  <div class="multiselect__container">
    <h2 class="multiselect__title">Build your perfect PUDGE</h2>
    <div class="multiselect__wrapper">
      <v-multiselect
        :list="filteredArtifacts"
        :header="chosenArtifacts"
        @select-item="addArtifactToHeader"
        @delete-item="deleteArtifactFromHeader"
      ></v-multiselect>
    </div>
  </div>
</template>

<script>
import VMultiselect from "@/components/VMultiselect.vue";

export default {
  name: "TheMultiselectContainer",
  components: {
    VMultiselect,
  },
  data: () => ({
    artifacts: [
      "Aeon Disk",
      "Armlet of Mordiggian",
      "Battle Fury",
      "Dagon",
      "Divine Rapier",
      "Mask of Madness",
      "Power Treads",
      "Shadow Blade",
    ],
    filteredArtifacts: [],
    chosenArtifacts: [],
  }),

  created() {
    this.filteredArtifacts = this.artifacts;
  },

  computed: {
    filterArtifacts() {
      this.filteredArtifacts = this.filteredArtifacts.filter((el) => {
        return !this.chosenArtifacts.includes(el);
      });
    },
  },

  methods: {
    addArtifactToHeader(event) {
      this.chosenArtifacts.push(event);
      this.filterArtifacts;
    },
    deleteArtifactFromHeader(event) {
      let i = this.chosenArtifacts.indexOf(event);
      this.chosenArtifacts.splice(i, 1);
      this.filteredArtifacts = this.artifacts.filter((el) => {
        return !this.chosenArtifacts.includes(el);
      });
    },
  },
};
</script>

<style scoped>
.multiselect__container {
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.multiselect__wrapper {
  width: 600px;
}
.multiselect__title {
  color: #fff;
  margin-bottom: 20px;
}
</style>
