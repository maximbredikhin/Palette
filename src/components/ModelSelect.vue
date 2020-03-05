<template>
  <div class="container">
    <div class="dropdown">
      <span class="dropdown__current">
        {{ currentModel.name }} — {{ currentModel.template }}
        <i class="dropdown__icon">▼</i>
      </span>
      <div class="dropdown__content">
        <span
          :class="[
            'dropdown__option',
            { dropdown__option_selected: model.name == currentModel.name }
          ]"
          v-for="(model, i) in models"
          :key="i"
          value="model"
          @click="pickModel(model)"
        >
          {{ model.name }} — {{ model.template }}
        </span>
      </div>
    </div>
    <div class="tip">{{ message }}</div>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  },
  data: () => ({
    // showTip: true,
    models: [
      { name: "#HEX", template: "#FF9800" },
      { name: "HEX", template: "FF9800" },
      { name: "RGB", template: "rgb(24, 75, 80)" },
      { name: "RGBA", template: "rgba(24, 75, 80, 1)" }
    ],
    currentModel: { name: "#HEX", template: "#FF9800" }
  }),
  methods: {
    async pickModel(model = this.currentModel) {
      this.currentModel = model;
      this.$emit("changeModel", this.currentModel.name);
    }
  },
  watch: {
    message: function() {
      document.querySelector(".tip").style.opacity = 1;
      setTimeout(() => {
        document.querySelector(".tip").style.opacity = 0;
      }, 1000);
    }
  },
  created: function() {
    this.$emit("changeModel", this.currentModel.name);
  }
};
</script>

<style lang="scss" scoped>
@keyframes show {
  from {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
.container {
  width: 100vw;
  height: 6rem;
  display: flex;
  justify-content: space-between;
  padding: 0 4.5rem;
}
.tip {
  display: inline-block;
  font-weight: 400;
  background-color: #505050dc;
  width: 100%;
  height: 2.25rem;
  font-family: "roboto", sans-serif;
  width: auto;
  color: #fff;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  box-shadow: 4px 6px 12px rgba(0, 0, 0, 0.12);
  opacity: 0;
  transition: opacity 0.5s ease;
}
.dropdown {
  position: relative;
  z-index: 10;
  display: inline-block;
  font-family: "roboto", sans-serif;
  width: 16rem;
  height: 2rem;
  cursor: pointer;
}
.dropdown__current {
  display: inline-block;
  font-weight: 400;
  background-color: #505050;
  width: 100%;
  height: 2.25rem;
  color: #fff;
  padding: 0.5rem;
  border-radius: 4px;
  box-shadow: 4px 6px 12px rgba(0, 0, 0, 0.12);
}
.dropdown__content {
  display: none;
  width: 100%;
  padding: 0.5rem 0;
  background-color: #fff;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
.dropdown:hover .dropdown__content {
  display: block;
}
.dropdown:hover .dropdown__current {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}
.dropdown__option {
  font-weight: 400;
  display: inline-block;
  padding: 0.2rem 1rem;
  width: 100%;
}
.dropdown__option_selected {
  font-weight: 500;
}
.dropdown__option:hover {
  background-color: #707070;
  color: #ffffff;
}
.dropdown__icon {
  float: right;
}
</style>
