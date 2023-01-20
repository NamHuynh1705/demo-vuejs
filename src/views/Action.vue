<template>
  <div id="Action">
    <div class="group-action">
      <div class="actions">
        <FontSize :fontSize="fontSize" @changeSize="handleChangeFontSize" />
      </div>
      <div class="actions">
        <Color :color="color" @changeColor="handleChangeColor" />
      </div>
      <div class="actions">
        <FontFamily :fontFamily="fontFamily" @changeFont="handleChangeFont" />
      </div>
    </div>
    <div class="text">
      <p
        :style="{
          fontSize: fontSize + 'px',
          color: color,
          fontFamily: fontFamily,
        }"
        class="text-setting"
      >
        Welcome to VueJS
      </p>
    </div>
  </div>
</template>

<script>
import FontSize from "../components/SettingText/FontSize.vue";
import Color from "../components/SettingText/Color.vue";
import FontFamily from "../components/SettingText/FontFamily.vue";
export default {
  name: "Action",
  data() {
    return {
      fontSize: 40,
      color: "black",
      fontFamily: "inherit",
    };
  },
  components: {
    FontSize,
    Color,
    FontFamily,
  },
  methods: {
    handleChangeFontSize(e) {
      this.fontSize = e.fontSize;
    },
    handleChangeColor(e) {
      this.color = e.color;
    },
    handleChangeFont(e) {
      this.fontFamily = e.fontFamily;
    },
  },
};
</script>

<style>
.group-action {
  border: 2px solid #22c786;
  width: 80%;
  height: 35vh;
  margin: 20px auto;
  display: flex;
  justify-content: space-around;
}
.text {
  width: 100%;
  height: 42vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.actions {
  margin-top: 40px;
}
.text p {
  font-weight: bold;
  font-style: italic;
}
</style>
