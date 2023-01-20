<template>
  <div class="container">
    <div id="employee-form">
      <b-form @submit.prevent="handleSubmit">
        <div class="label-input label-input-1">
          <label>Employee Name: </label>
          <b-form-input
            style="width: 270px; height: 35px"
            ref="first"
            type="text"
            :class="{ 'has-error': submitting && invalidName }"
            v-model="employee.name"
            @focus="clearStatus"
            @keypress="clearStatus"
          ></b-form-input>
        </div>
        <div class="label-input label-input-2">
          <label>Employee Email: </label>
          <b-form-input
            style="width: 270px; height: 35px"
            type="text"
            :class="{ 'has-error': submitting && invalidEmail }"
            v-model="employee.email"
            @focus="clearStatus"
          ></b-form-input>
        </div>
        <p v-if="error && submitting" class="error-message">
          ❗ Please fill out all required fields
        </p>
        <p v-if="success" class="success-message">
          ✅ Employee successfully added
        </p>
        <button class="button-add-employ">
          <b-icon icon="plus-circle"></b-icon>&nbsp;Add
        </button>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "EmployeeForm",
  data() {
    return {
      error: false,
      submitting: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },
  },
  methods: {
    handleSubmit() {
      this.clearStatus();
      this.submitting = true;

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:employee", this.employee);
      this.$refs.first.focus();
      this.employee = {
        name: "",
        email: "",
      };
      this.clearStatus();
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
};
</script>

<style scoped>
.label-input {
  display: flex;
  justify-content: center;
  align-items: center;
}
.label-input-1 {
  margin-bottom: 7px;
}
.label-input label {
  min-width: 125px;
}
.button-add-employ {
  margin-top: 10px !important;
  margin: auto;
  transform: translate(212%, 0);
  display: block;
  font-weight: 400;
  text-align: center;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}
form {
  margin-bottom: 1rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
  display: flex;
  justify-content: center;
  margin-bottom: 0px;
  margin-top: 5px;
}

.success-message {
  color: #32a95d;
  display: flex;
  justify-content: center;
  margin-bottom: 0px;
  margin-top: 5px;
}
</style>
