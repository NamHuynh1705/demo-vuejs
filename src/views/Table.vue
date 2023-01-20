<template>
  <div id="Table">
    <div class="col-4 form-action">
      <FormAction
        :dataForm="dataForm"
        :model="model"
        @handleModel="handleModel"
        @handleReset="handleReset"
        @addDataForm="addDataForm"
        @editDataForm="editDataForm"
      />
    </div>
    <div class="col-8 table-list">
      <InputSearch :searchText="searchText" @handleSearch="handleSearch" />
      <TableList
        :heads="heads"
        :list="list"
        :model="model"
        :text="text"
        :dataForm="dataForm"
        @handleEdit="handleEdit"
        @handleModel="handleModel"
        @handleDataForm="handleDataForm"
        @handleDelete="handleDelete"
        :resultSearch="resultSearch"
      />
    </div>
  </div>
</template>

<script>
import FormAction from "../components/Table/FormAction.vue";
import TableList from "../components/Table/TableList.vue";
import InputSearch from "../components/Table/InputSearch.vue";
export default {
  name: "Table",
  data() {
    return {
      heads: ["#", "Smartphone", "Company", "Launch year", "Actions"],
      list: [
        {
          id: 1,
          phoneName: "Galaxy S21",
          company: "Samsung",
          year: "2021",
        },
        {
          id: 2,
          phoneName: "Iphone 11",
          company: "Apple",
          year: "2019",
        },
        {
          id: 3,
          phoneName: "Iphone 12",
          company: "Apple",
          year: "2020",
        },
        {
          id: 4,
          phoneName: "Xiaomi Mi 11",
          company: "Xiaomi",
          year: "2021",
        },
        {
          id: 5,
          phoneName: "Nokia 5.1 plus",
          company: "Nokia",
          year: "2019",
        },
      ],
      model: "Add",
      text: {},
      dataForm: {
        id: "",
        phoneName: "",
        company: "",
        year: "",
      },
      searchText: "",
    };
  },
  components: {
    FormAction,
    TableList,
    InputSearch,
  },
  methods: {
    handleEdit(e) {
      this.text = e.text;
    },
    handleModel(e) {
      this.model = e.model;
    },
    handleDataForm(e) {
      this.dataForm = e.dataForm;
    },
    handleDelete(e) {
      this.list = e.list;
    },
    handleReset(e) {
      this.dataForm = e.dataForm;
    },
    addDataForm(e) {
      this.dataForm = JSON.parse(JSON.stringify(e.dataForm));
      let listArr = this.list;
      this.dataForm.id = this.list.length + 1;
      listArr.push(this.dataForm);
    },
    editDataForm(e) {
      this.dataForm = e.dataForm;
      this.list = JSON.parse(
        JSON.stringify(
          this.list.map((item) => {
            if (item.id == this.dataForm.id) return this.dataForm;
            else return item;
          })
        )
      );
    },
    handleSearch(e) {
      this.searchText = e;
    },
  },
  computed: {
    resultSearch() {
      if (this.searchText) {
        return this.list.filter((item) => {
          return this.searchText
            .toLowerCase()
            .split(" ")
            .every((u) => item.phoneName.toLowerCase().includes(u));
        });
      }
      return this.list;
    },
  },
};
</script>

<style>
.form-action {
  height: 100vh;
  float: left;
}
.table-list {
  height: 100vh;
  float: right;
  position: unset;
}
</style>
