<template>
  <div>
    <h3>Change FontSize</h3>
    <div class="group-fontsize">
      <b-button
        variant="danger"
        class="mb-2"
        @keyup.down="minusSize"
        @click="minusSize"
        :disabled="this.fontSize == 10"
      >
        <b-icon icon="dash" aria-hidden="true"></b-icon>
      </b-button>
      <p class="font-size">{{ fontSize + "px" }}</p>
      <b-button
        variant="primary"
        class="mb-2"
        @keyup.up="plusSize"
        @click="plusSize"
        :disabled="this.fontSize == 100"
      >
        <b-icon icon="plus" aria-hidden="true"></b-icon>
      </b-button>
    </div>
  </div>
</template>
<script>
export default {
  name: "FontSize",
  data() {
    return {};
  },
  props: {
    fontSize: Number,
  },
  methods: {
    plusSize() {
      let data = {
        fontSize: this.fontSize + 2,
      };
      this.$emit("changeSize", data);
    },
    minusSize() {
      let data = {
        fontSize: this.fontSize > 2 && this.fontSize - 2,
      };
      this.$emit("changeSize", data);
    },
  },
};
</script>

<style>
.group-fontsize {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
}
.font-size {
  margin-left: 15px;
  margin-right: 15px;
}
.mb-2 {
  font-weight: bold;
}
</style>