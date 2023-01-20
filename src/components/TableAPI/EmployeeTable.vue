<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
    <table v-else class="table table-hover table-phone">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="employee.id" v-for="employee in employees">
          <td v-if="editing === employee.id">
            <b-form-input v-model="employee.name" type="text"></b-form-input>
          </td>
          <td v-else>{{ employee.name }}</td>
          <td v-if="editing === employee.id">
            <b-form-input v-model="employee.email" type="email"></b-form-input>
          </td>
          <td v-else>{{ employee.email }}</td>
          <td v-if="editing === employee.id">
            <b-button @click="editEmployee(employee)" variant="success"
              >Save</b-button
            >
            <b-button @click="editing = null">Cancel</b-button>
          </td>
          <td v-else>
            <b-button @click="editMode(employee.id)" variant="primary"
              >Edit</b-button
            >
            <b-button 
              @click="$emit('delete:employee', employee.id)"
              variant="danger"
              >Delete</b-button
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "EmployeeTable",
  props: {
    employees: Array,
  },
  data() {
    return {
      editing: null,
    };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },

    editEmployee(employee) {
      if (employee.name === "" || employee.email === "") return;
      this.$emit("edit:employee", employee.id, employee);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
#employee-table {
  overflow-y: auto;
  max-height: 440px;
}
button {
  margin: 0 0.5rem 0 0;
}

input {
  margin: 0;
}

.empty-table {
  text-align: center;
}

::-webkit-scrollbar-track {
  border-radius: 10px;
  background-color: #f5f5f5;
}
::-webkit-scrollbar {
  width: 12px;
  background-color: #f5f5f5;
}
::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #737373a1;
}
</style>
