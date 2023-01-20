<template>
  <div class="group-input">
    <label class="label-add">{{ model }}</label>
    <div>
      <b-form @submit="onSubmit" @reset="onReset">
        <b-form-group label="Smartphone:">
          <b-form-input
            v-model="dataForm.phoneName"
            type="text"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group label="Company:">
          <b-form-input
            v-model="dataForm.company"
            type="text"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group label="Launch year:">
          <b-form-input
            v-model="dataForm.year"
            type="text"
            required
          ></b-form-input>
        </b-form-group>
        <div class="two-button">
          <b-button class="button-save" type="submit" variant="primary"
            >Save</b-button
          >
          <b-button
            class="button-cancel"
            type="reset"
            variant="secondary"
            @click="setModelAdd('Add')"
            >Cancel</b-button
          >
        </div>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "FormAction",
  data() {
    return {};
  },
  props: {
    model: String,
    dataForm: Object,
  },

  methods: {
    setModelAdd(model) {
      let data = {
        model: model,
      };
      this.$emit("handleModel", data);
    },
    onSubmit(event) {
      if (this.model == "Add") {
        event.preventDefault();
        let data = {
          dataForm: this.dataForm,
        };
        this.$emit("addDataForm", data);
      } else if (this.model == "Edit") {
        event.preventDefault();
        let data = {
          dataForm: this.dataForm,
        };
        this.$emit("editDataForm", data);
      }
    },
    onReset(event) {
      event.preventDefault();
      let data = {
        dataForm: {},
      };
      this.$emit("handleReset", data);
    },
  },
};
</script>

<style>
.group-input {
  margin: auto;
  width: 80%;
  padding: 10px 15px 10px 15px;
  border: 1px solid #51e1a7;
  box-shadow: 1px 1px 5px #7ce9bd;
  border-radius: 15px;
  margin-top: 40px;
  background-color: #f1f1f157;
}
.label-add {
  font-size: 30px;
  font-weight: bold;
  font-style: italic;
  color: #22c786;
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
}
.two-button {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  margin-bottom: 10px;
}
.button-cancel {
  margin-left: 7px;
}
.button-save {
  margin-right: 7px;
}
</style>