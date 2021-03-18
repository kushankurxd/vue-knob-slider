<template>
  <div class="main-container" @mousedown="unselectKnob">
    <div class="title-container">
      <h2 class="title">Knob Sliders</h2>
    </div>

    <div class="knob-container">
      <div class="knob" v-for="(knob, index) in accelKnobs" :key="index">
        <Knob :knob="knob" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Knob from "./components/knob.vue";

@Component({
  components: {
    Knob,
  },
})
export default class App extends Vue {
  unselectKnob() {
    for (let i = 0; i < this.accelKnobs.length; i++) {
      if (this.accelKnobs[i].selected) {
        this.accelKnobs[i].selected = false;
      }
    }
  }
  selectedKnob = 0;
  accelKnobs = [
    {
      id: 0,
      label: "Knob 1",
      rotation: -132,
      color: "#e9c46a",
      active: true,
      selected: false,
      style: 1,
      value: 0,
    },

    {
      id: 0,
      label: "Knob 2",
      rotation: -132,
      color: "#e63946",
      active: true,
      selected: false,
      style: 3,
      value: 0,
    },

    {
      id: 0,
      label: "Knob 3",
      rotation: -132,
      color: "#ffba08",
      active: true,
      selected: false,
      style: 2,
      value: 0,
    },
  ];
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap");
* {
  font-family: "Poppins";
}
body {
  background: #264653;
  overflow: hidden;
}

.main-container {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  display: flex;
  flex-flow: column;
  justify-content: center;
  margin-top: -44px;
}

.title-container {
  display: flex;
  justify-content: center;
}

.title {
  color: #fff;
  letter-spacing: 1px;
}

.knob-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-top: 34px;
}

.knob {
  color: #fff;
}
</style>