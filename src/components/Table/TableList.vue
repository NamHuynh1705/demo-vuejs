<template>
  <div>
    <table class="table table-hover table-phone">
      <thead>
        <tr>
          <th v-for="(head, index) in heads" :key="index">
            {{ head }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(text, index) in resultSearch" :key="index">
          <td>{{ text.id }}</td>
          <td>{{ text.phoneName }}</td>
          <td>{{ text.company }}</td>
          <td>{{ text.year }}</td>
          <td>
            <b-icon
              class="icon-action action-edit"
              icon="pencil-square"
              variant="success"
              @click="handleEdit(text, 'Edit')"
            ></b-icon>
            <b-icon
              class="icon-action"
              icon="trash-fill"
              variant="danger"
              @click="handleDelete(text)"
            ></b-icon>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TableList",
  data() {
    return {};
  },
  props: {
    heads: Array,
    list: Array,
    model: String,
    text: Object,
    dataForm: Object,
    resultSearch: Array,
  },
  methods: {
    handleEdit(text, model) {
      let data = {
        text: text,
      };
      this.$emit("handleEdit", data);
      let dataModel = {
        model: model,
      };
      this.$emit("handleModel", dataModel);
      let setDataForm = {
        dataForm: JSON.parse(JSON.stringify(text)),
      };
      this.$emit("handleDataForm", setDataForm);
    },
    handleDelete(text) {
      let dataArr = this.list;
      let filterData = dataArr.filter((value) => value.id !== text.id);
      let dataDetele = {
        list: filterData,
      };
      this.$emit("handleDelete", dataDetele);
    },
  },
};
</script>

<style>
.table-phone {
  margin-top: 10px;
}
.icon-action {
  font-size: 23px;
  cursor: pointer;
}
.action-edit {
  margin-right: 10px;
}
</style>