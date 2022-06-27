<template>
  <div class="container">
    <div class="modals">
      <button class="btn btn-int" @click="isOpenModalDazzle = true">
        dazzle
      </button>
      <button class="btn btn-str" @click="isOpenModalAxe = true">axe</button>
      <button class="btn btn-agi" @click="isOpenModalSniper = true">
        sniper
      </button>
      <button class="btn btn-str" @click="isOpenModalRoshan = true">
        roshan
      </button>
    </div>
    <div class="dropdowns">
      <div class="wrapper">
        <v-dropdown
          :list="position.filteredValues"
          :header="position.currentValue"
          @change-header="changePosition($event)"
        ></v-dropdown>
      </div>
      <div class="wrapper">
        <v-dropdown
          :list="heroes.filteredValues"
          :header="heroes.currentValue"
          @change-header="changeHeroes($event)"
        ></v-dropdown>
      </div>
    </div>

    <!-- modals -->
    <v-modal v-if="isOpenModalDazzle" @close-modal="closeModal">
      <template v-slot:header>
        <div class="modal__header">
          <div class="modal__stat">
            <img
              src="@/assets/img/hero_intelligence.png"
              class="modal__stat-icon"
              alt="intelligence"
            />
            <h2 class="modal__stat-title">intelligence</h2>
          </div>
          <h1 class="modal__title">dazzle</h1>
          <h2 class="modal__subtitle">
            Powerful healer who can briefly prevent death
          </h2>
        </div>
      </template>

      <p class="modal__text">
        Born to support his cohorts in battle, Dazzle
        <strong>keeps wounded allies alive</strong> so they might later rain
        death upon the enemy. His <strong>strange magic</strong> weaves its way
        into <strong>nearby armor</strong>, weakening enemies and strengthening
        friends.
      </p>
      <a href="https://www.dota2.com/hero/dazzle" class="modal__link"
        >Read Full Information</a
      >

      <template v-slot:footer>
        <div class="modal__footer">
          <div class="modal__block">
            <h4 class="modal__headline">attack type</h4>
            <div class="modal__type">
              <img
                class="modal__type-icon"
                src="@/assets/img/ranged.svg"
                alt="ranged"
              />
              <p class="modal__type-text">ranged</p>
            </div>
          </div>
          <div class="modal__block">
            <h4 class="modal__headline">complexity</h4>
            <div class="modal__complexity">
              <div class="modal__rhombus fill"></div>
              <div class="modal__rhombus"></div>
              <div class="modal__rhombus"></div>
            </div>
          </div>
        </div>
      </template>

      <template v-slot:aside>
        <img src="@/assets/img/dazzle.png" class="modal__img" alt="dazzle" />
      </template>
    </v-modal>
    <v-modal v-if="isOpenModalAxe" @close-modal="closeModal">
      <template v-slot:header>
        <div class="modal__header">
          <div class="modal__stat">
            <img
              src="@/assets/img/hero_strength.png"
              class="modal__stat-icon"
              alt="strength"
            />
            <h2 class="modal__stat-title">strenght</h2>
          </div>
          <h1 class="modal__title">axe</h1>
          <h2 class="modal__subtitle">
            Taunts and forces enemies to attack him
          </h2>
        </div>
      </template>

      <p class="modal__text">
        One after another, Axe cuts down his foes. Marching ahead of his team,
        he
        <strong>locks his enemies in battle</strong> then counters their blows
        with a <strong>deadly spin</strong> of his weapon. Slamming his
        <strong>culling blade</strong> through a weakened enemy, he is always
        charging onward.
      </p>
      <a href="https://www.dota2.com/hero/axe" class="modal__link"
        >Read Full Information</a
      >

      <template v-slot:footer>
        <div class="modal__footer">
          <div class="modal__block">
            <h4 class="modal__headline">attack type</h4>
            <div class="modal__type">
              <img
                class="modal__type-icon"
                src="@/assets/img/melee.svg"
                alt="melee"
              />
              <p class="modal__type-text">melee</p>
            </div>
          </div>
          <div class="modal__block">
            <h4 class="modal__headline">complexity</h4>
            <div class="modal__complexity">
              <div class="modal__rhombus fill"></div>
              <div class="modal__rhombus"></div>
              <div class="modal__rhombus"></div>
            </div>
          </div>
        </div>
      </template>

      <template v-slot:aside>
        <img src="@/assets/img/axe.png" class="modal__img" alt="axe" />
      </template>
    </v-modal>
    <v-modal v-if="isOpenModalSniper" @close-modal="closeModal">
      <template v-slot:header>
        <div class="modal__header">
          <div class="modal__stat">
            <img
              src="@/assets/img/hero_agility.png"
              class="modal__stat-icon"
              alt="agility"
            />
            <h2 class="modal__stat-title">agility</h2>
          </div>
          <h1 class="modal__title">sniper</h1>
          <h2 class="modal__subtitle">picks off his enemies from afar</h2>
        </div>
      </template>

      <p class="modal__text">
        <strong>Death from a distance</strong> is Sniper's specialty. He keeps
        his enemies on their toes with a steady barrage of firepower, and then,
        when the time is right, picks them off with a
        <strong>kill shot.</strong>
      </p>
      <a href="https://www.dota2.com/hero/sniper" class="modal__link"
        >Read Full Information</a
      >

      <template v-slot:footer>
        <div class="modal__footer">
          <div class="modal__block">
            <h4 class="modal__headline">attack type</h4>
            <div class="modal__type">
              <img
                class="modal__type-icon"
                src="@/assets/img/ranged.svg"
                alt="ranged"
              />
              <p class="modal__type-text">ranged</p>
            </div>
          </div>
          <div class="modal__block">
            <h4 class="modal__headline">complexity</h4>
            <div class="modal__complexity">
              <div class="modal__rhombus fill"></div>
              <div class="modal__rhombus"></div>
              <div class="modal__rhombus"></div>
            </div>
          </div>
        </div>
      </template>

      <template v-slot:aside>
        <img src="@/assets/img/sniper.png" class="modal__img" alt="sniper" />
      </template>
    </v-modal>
    <v-modal v-if="isOpenModalRoshan" @close-modal="closeModal">
      <template v-slot:header>
        <div class="modal__header">
          <h1 class="modal__title">roshan</h1>
          <h2 class="modal__subtitle">"tobi pizda"</h2>
        </div>
      </template>

      <p class="modal__text">You better <strong>run</strong></p>
      <a
        href="https://dota2.fandom.com/ru/wiki/%D0%A0%D0%BE%D1%88%D0%B0%D0%BD"
        class="modal__link"
        >Read Full Information</a
      >

      <template v-slot:footer>
        <div class="modal__footer">
          <div class="modal__block">
            <h4 class="modal__headline">attack type</h4>
            <div class="modal__type">
              <img
                class="modal__type-icon"
                src="@/assets/img/melee.svg"
                alt="melee"
              />
              <p class="modal__type-text">melee</p>
            </div>
          </div>
          <div class="modal__block">
            <h4 class="modal__headline">complexity</h4>
            <div class="modal__complexity">
              <div class="modal__rhombus fill"></div>
              <div class="modal__rhombus fill"></div>
              <div class="modal__rhombus fill"></div>
            </div>
          </div>
        </div>
      </template>

      <template v-slot:aside>
        <img src="@/assets/img/roshan.png" class="modal__img" alt="roshan" />
      </template>
    </v-modal>
  </div>
</template>

<script>
import VDropdown from "@/components/VDropdown.vue";
import VModal from "@/components/VModal.vue";

export default {
  name: "App",
  components: {
    VDropdown,
    VModal,
  },

  data: () => ({
    position: {
      values: [
        "Carry",
        "Mid Core",
        "Offlaner",
        "Semi-Support",
        "Main-Support",
        "Ruiner",
      ],
      currentValue: "Choose your position",
      filteredValues: [],
    },

    heroes: {
      values: [
        "Axe",
        "Dazzle",
        "Juggernaut",
        "Lion",
        "Monkey King",
        "Sniper",
        "Creep",
        "Roshan",
      ],
      currentValue: "Pick your hero",
      filteredValues: [],
    },

    isOpenModalDazzle: false,
    isOpenModalAxe: false,
    isOpenModalSniper: false,
    isOpenModalRoshan: false,
  }),

  created() {
    this.position.filteredValues = this.position.values;
    this.heroes.filteredValues = this.heroes.values;
  },

  methods: {
    // Можно ли сделать эти методы одним уникальным методом?
    // Например, принимать в функции слова типа "position", "heroes" и т.д?

    changePosition(event) {
      this.position.currentValue = event.target.textContent;
      this.position.filteredValues = this.position.values.filter(
        (el) => el !== this.position.currentValue
      );
    },
    changeHeroes(event) {
      this.heroes.currentValue = event.target.textContent;
      this.heroes.filteredValues = this.heroes.values.filter(
        (el) => el !== this.heroes.currentValue
      );
    },

    // Модалки
    closeModal() {
      this.isOpenModalDazzle = false;
      this.isOpenModalAxe = false;
      this.isOpenModalSniper = false;
      this.isOpenModalRoshan = false;
    },
  },
};
</script>

<style>
@font-face {
  font-family: "Poppins";
  src: url("@/assets/fonts/Poppins-Medium.woff2") format("woff2"),
    url("@/assets/fonts/Poppins-Medium.woff") format("woff"),
    url("@/assets/fonts/Poppins-Medium.ttf") format("truetype");
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}

* {
  padding: 0;
  margin: 0;
  border: 0;
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  background-color: #333;
  background-image: url(assets/img/bg.jpg);
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  font-family: "Poppins", sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 140%;
}

ul li {
  list-style: none;
}

.container {
  position: relative;
  width: 100%;
  padding-top: 150px;
}

.dropdowns {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  gap: 0 40px;
}

.wrapper {
  width: 300px;
}

.modals {
  display: flex;
  justify-content: center;
  gap: 0 40px;
}

.btn {
  padding: 8px 16px;
  background-color: transparent;
  border-radius: 6px;
  border: 2px solid #fff;
  cursor: pointer;

  font-family: "Poppins", sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  color: #fff;
  text-transform: uppercase;

  transition: all 0.15s ease;
}

.btn-str:hover {
  background-color: #ec3d06;
  transition: all 0.15s ease;
}

.btn-int:hover {
  background-color: #02cbde;
  transition: all 0.15s ease;
}

.btn-agi:hover {
  background-color: #26e030;
  transition: all 0.15s ease;
}
</style>
