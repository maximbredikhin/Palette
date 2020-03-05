<template>
  <div class="picker">
    <div class="picker__colors">
      <div
        class="color color_left"
        :style="{ backgroundColor: this.color.hex[0] }"
        @click="pickColor"
      ></div>
      <div
        class="color color_center"
        :style="{ backgroundColor: this.color.hex[1] }"
        @click="pickColor"
      ></div>
      <div
        class="color color_right"
        :style="{ backgroundColor: this.color.hex[2] }"
        @click="pickColor"
      ></div>
    </div>
    <span class="picker__description">{{ this.color.name }}</span>
  </div>
</template>

<script>
import { log } from "util";
export default {
  props: {
    color: {
      type: Object,
      required: true
    },
    model: {
      type: String,
      required: true
    }
  },
  data: () => ({}),
  methods: {
    async pickColor(event) {
      let rgb = event.target.style.backgroundColor;
      let rgbArray = rgb.slice(4, -1).split(", ");
      let output = "";
      if (this.model == "RGB") {
        output = rgb;
      } else if (this.model == "RGBA") {
        output = `rgba(${rgbArray[0]}, ${rgbArray[1]}, ${rgbArray[2]}, 1)`;
      } else if (this.model == "HEX") {
        output = rgbArray.map(e => (+e).toString(16).padStart(2, "0")).join("");
      } else if (this.model == "#HEX") {
        output =
          "#" + rgbArray.map(e => (+e).toString(16).padStart(2, "0")).join("");
      }
      navigator.clipboard
        .writeText(output)
        .then(() => {
          this.$emit("pick", output);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.picker {
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  height: 5.25rem;
  width: 12rem;
  margin: 1rem 1.5rem;
  border-radius: 4px;
  box-shadow: 4px 6px 12px rgba(0, 0, 0, 0.12);
  // transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}
.picker__colors {
  height: 60%;
  width: 100%;
  display: flex;
}
.color {
  width: 33.3%;
  height: 100%;
  cursor: crosshair;
  transition: all 0.2s ease-out;
}
.color:hover {
  width: 50%;
}
.picker__description {
  font-family: "roboto", sans-serif;
  font-weight: 500;
  font-size: 1rem;
  padding: 0.5rem;
  color: #3b3b3b;
}
.color_left {
  border-top-left-radius: 4px;
}
.color_right {
  border-top-right-radius: 4px;
}
</style>
