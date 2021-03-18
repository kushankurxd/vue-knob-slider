<template>
  <div class="rela-block">
    <div
      class="knob-active-light"
      :style="{ 'background-color': knob.active ? knob.color : '#888' }"
    ></div>
    <div :class="['rela-inline', 'knob', 'style' + knob.style]">
      <div
        class="rela-block knob-dial"
        :style="{ color: knob.active ? knob.color : '#888' }"
      >
        <div
          class="abs-center dial-grip"
          :style="{
            transform: 'translate(-50%,-50%) rotate(' + knob.rotation + 'deg)',
          }"
          @click="selectKnob"
        ></div>
        <svg class="dial-svg" viewBox="0 0 100 100">
          <path d="M20,76 A 40 40 0 1 1 80 76" fill="none" stroke="#55595C" />
          <path
            d="M20,76 A 40 40 0 1 1 80 76"
            fill="none"
            :stroke="knob.active ? knob.color : '#888'"
            :style="{
              'stroke-dashoffset':
                184 - 184 * ((knob.rotation * 1 + 132) / 264),
            }"
          />
        </svg>
      </div>
      <div class="rela-block knob-label">
        {{ knob.value }}
      </div>
      <div class="rela-block knob-label">
        {{ knob.label }}
      </div>
    </div>
  </div>
</template>


<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
@Component
export default class Knob extends Vue {
  @Prop() knob!: any;
  @Prop() unselectKnob!: any;
  currentY = 0;
  currentX = 0;
  mousemoveFunction = (e: any) => {
    if (this.knob.selected) {
      // Knob Rotation
      if (e.pageY - this.currentY !== 0) {
        this.knob.rotation -= e.pageY - this.currentY;
      }
      this.currentY = e.pageY;
      if (-e.pageX - this.currentX !== 0) {
        this.knob.rotation -= -e.pageX - this.currentX;
      }
      this.currentX = -e.pageX;
      // Setting Max rotation
      if (this.knob.rotation >= 132) {
        this.knob.rotation = 132;
        this.knob.value = 132;
      } else if (this.knob.rotation <= -132) {
        this.knob.rotation = -132;
        this.knob.value = -132;
      } else {
        this.knob.value = this.knob.rotation;
      }
    }
  };
  selectKnob() {
    this.knob.selected = true;
    this.knob.active = true;
  }
  mounted() {
    window.addEventListener("mousemove", this.mousemoveFunction);
  }
}
</script>

<style scoped>
.abs-center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.rela-block {
  display: block;
  position: relative;
}
.rela-inline {
  display: inline-block;
  position: relative;
}
.knob {
  border-radius: 3px;
  padding: 24px 20px;
  padding-bottom: 4px;
  margin: 0 10px 10px 0;
  text-align: center;
}
.knob.style1 .dial-grip {
  height: 72px;
  width: 72px;
  border: 6px solid #181b1c;
}
.knob.style1 .dial-grip::after {
  position: absolute;
  top: 5px;
  left: 50%;
  height: 10px;
  background-color: #e4e8ea;
}
.knob.style2 .dial-svg {
  stroke-width: 2.5;
}
.knob.style2 .dial-grip {
  height: 60px;
  width: 60px;
  background-color: #888;
}
.knob.style2 .dial-grip::after {
  height: 15px;
  background-color: #2c2d2f;
}
.knob.style3 .dial-svg {
  stroke-width: 2.75;
}
.knob.style3 .dial-grip {
  z-index: 5;
  height: 82px;
  width: 82px;
  transition: 0.3s cubic-bezier(0, 0, 0.24, 1);
}
.knob.style3 .dial-grip::after {
  height: 25px;
  width: 3px;
  border-radius: 4px;
  background-color: currentColor;
}
.knob-active-light {
  position: absolute;
  top: 12px;
  left: 12px;
  height: 10px;
  width: 10px;
  border-radius: 100%;
}
.knob-dial {
  height: 100px;
  width: 100px;
  text-align: left !important;
  transition: 0s;
}
.dial-grip {
  border-radius: 100%;
  transition: 0s;
}
.dial-grip::after {
  content: "";
  position: absolute;
  top: 0;
  left: 50%;
  width: 2px;
  transform: translateX(-50%);
}
.dial-svg {
  pointer-events: none;
  position: absolute;
  stroke-width: 8;
  stroke-dasharray: 184 184;
  stroke-linecap: round !important;
}
.dial-svg path {
  transition: 0.3s cubic-bezier(0, 0, 0.24, 1);
}
.knob-label {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
</style>