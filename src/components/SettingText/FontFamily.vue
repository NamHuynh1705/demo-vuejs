<template>
  <div>
    <h3>Change FontFamily</h3>
    <div class="group-font">
      <select id="fonts" v-model="selected" @change="setSelected(font)">
        <option
          v-for="(font, index) in fontfamily"
          :key="index"
          :value="font"
          :selected="{ index }"
        >
          {{ font }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "FontFamily",
  components: {},
  props: {
    fontFamily: String,
  },
  data() {
    return {
      fontfamily: [
        "inherit",
        "serif",
        "cursive",
        "system-ui",
        "Impact,Charcoal,sans-serif",
      ],
      selected: "",
    };
  },
  methods: {
    setSelected() {
      let data = {
        fontFamily: this.selected,
      };
      this.$emit("changeFont", data);
    },
  },
};
</script>

<style>
select {
  text-transform: uppercase;
  padding: 5px 10px;
  /* margin-top: 5px; */
}
option {
  background-color: #f1f1f1;
}
.group-font {
  margin-top: 15px;
}
</style>