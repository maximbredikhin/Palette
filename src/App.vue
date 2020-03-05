<template>
  <div id="app">
    <model-select class="select" @changeModel="changeMod" :message="message"></model-select>
    <picker
      v-for="(color, index) in colors"
      :key="index"
      :color="color"
      :model="model"
      @pick='pick' 
    ></picker>
  </div>
</template>

<script>
import picker from "./components/Picker.vue";
import modelSelect from "./components/ModelSelect.vue";

export default {
  name: "app",
  components: {
    picker,
    modelSelect
  },
  data: () => ({
    message: '',
    model: "",
    colors: [
      {
        name: "Red",
        hex: ["#ef9a9a", "#f44336", "#c62828"]
      },
      {
        name: "Pink",
        hex: ["#F48FB1", "#E91E63", "#AD1457"]
      },
      {
        name: "Purple",
        hex: ["#CE93D8", "#9C27B0", "#6A1B9A"]
      },
      {
        name: "Deep Purple",
        hex: ["#B39DDB", "#673AB7", "#4527A0"]
      },
      {
        name: "Indigo",
        hex: ["#9FA8DA", "#3F51B5", "#283593"]
      },
      {
        name: "Blue",
        hex: ["#90CAF9", "#2196F3", "#1565C0"]
      },
      {
        name: "Light Blue",
        hex: ["#81D4FA", "#03A9F4", "#0277BD"]
      },
      {
        name: "Cyan",
        hex: ["#80DEEA", "#00BCD4", "#00838F"]
      },

      {
        name: "Teal",
        hex: ["#80CBC4", "#009688", "#00695C"]
      },
      {
        name: "Green",
        hex: ["#A5D6A7", "#4CAF50", "#2E7D32"]
      },
      {
        name: "Light Green",
        hex: ["#C5E1A5", "#8BC34A", "#558B2F"]
      },
      {
        name: "Lime",
        hex: ["#E6EE9C", "#CDDC39", "#9E9D24"]
      },
      {
        name: "Yellow",
        hex: ["#FFF59D", "#FFEB3B", "#F9A825"]
      },
      {
        name: "Amber",
        hex: ["#FFE082", "#FFC107", "#FF8F00"]
      },
      {
        name: "Orange",
        hex: ["#FFCC80", "#FF9800", "#EF6C00"]
      },
      {
        name: "Deep Orange",
        hex: ["#FFAB91", "#FF5722", "#D84315"]
      },
      {
        name: "Brown",
        hex: ["#BCAAA4", "#795548", "#4E342E"]
      },
      {
        name: "Grey",
        hex: ["#EEEEEE", "#9E9E9E", "#424242"]
      },
      {
        name: "Blue Grey",
        hex: ["#B0BEC5", "#607D8B", "#37474F"]
      }
    ]
  }),
  methods: {
    changeMod(mod) {
      this.model = mod;
    },
    pick(str) {
      this.message = str + ' copied';
    }
  }
};
</script>

<style lang="scss">
*,
::before,
::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #f1f1f1;
}
#app {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 5% 10%;
}
</style>
