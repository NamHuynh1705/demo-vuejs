<template>
  <div id="app" class="small-container">
    <h2 class="label-employ">Employees</h2>

    <employee-form @add:employee="addEmployee" />
    <employee-table
      :employees="employees"
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />
  </div>
</template>

<script>
import EmployeeTable from "../components/TableAPI/EmployeeTable.vue";
import EmployeeForm from "../components/TableAPI/EmployeeForm.vue";

export default {
  name: "TableAPI",
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [],
    };
  },

  mounted() {
    this.getEmployees();
  },

  methods: {
    async getEmployees() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );
        const data = await response.json();
        this.employees = data;
      } catch (error) {
        console.error(error);
      }
    },

    async addEmployee(employee) {
      // Biến đổi hàm thành 1 hàm Promise(bất đồng bộ)
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users",
          {
            method: "POST",
            body: JSON.stringify(employee),
            headers: { "Content-type": "application/json; charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.employees = [...this.employees, data];
      } catch (error) {
        console.error(error);
      }
    },

    async editEmployee(id, updatedEmployee) {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users/${id}`,
          {
            method: "PUT",
            body: JSON.stringify(updatedEmployee),
            headers: { "Content-type": "application/json; charset=UTF-8" },
          }
        );
        const data = await response.json();
        this.employees = this.employees.map((employee) =>
          employee.id === id ? data : employee
        );
      } catch (error) {
        console.error(error);
      }
    },

    async deleteEmployee(id) {
      try {
        await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
          method: "DELETE",
        });
        this.employees = this.employees.filter(
          (employee) => employee.id !== id
        );
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style>
.label-employ {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
  margin-top: 5px;
  color: #22c786;
  text-shadow: 0px 1px #22c786;
  font-style: italic;
}
button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 700px;
  margin: auto;
}
</style>
