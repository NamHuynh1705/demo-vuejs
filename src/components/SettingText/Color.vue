<template>
  <div class="change-color">
    <h3>Change Color</h3>
    <div class="group-color">
      <div class="button-color" v-for="(color, index) in colors" :key="index">
        <div
          :style="{ backgroundColor: color }"
          @click="setActive(color, index)"
          :class="{ active: activeColor == index }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Color",
  data() {
    return {
      colors: ["red", "blue", "yellow", "green", "gray", "pink"],
      isActive: false,
      activeColor: 0,
    };
  },
  props: {
    color: String,
  },
  methods: {
    setActive(color, index) {
      this.activeColor = index;
      let data = {
        color: color,
      };
      this.$emit("changeColor", data);
    },
  },
};
</script>

<style>
.change-color {
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  align-items: center;
}
.group-color {
  display: flex;
  flex-flow: row wrap;
  align-content: space-between;
  justify-content: space-between;
  width: 206px;
  margin-top: 3px;
}
.button-color {
  margin: 7px;
  cursor: pointer;
}
.button-color div {
  width: 45px;
  height: 45px;
}
.active {
  border: 3px solid #000;
  box-shadow: 1px 2px 5px #000;
}
</style>