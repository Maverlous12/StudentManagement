<template>
  <table class="table">
    <thead class="table__list--head">
      <tr class="table__list--detail">
        <th>ID</th>
        <th>NAME</th>
        <th>AGE</th>
        <th>CLASS</th>
        <th>ADDRESS</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody class="table__list--body">
      <tr class="table__list--detail" v-for="user in list" v-bind:key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
        <td>{{ user.age }}</td>
        <td>{{ user.class }}</td>
        <td>{{ user.address }}</td>
        <td>
          <b-button
            v-b-modal.modal-prevent-closing
            variant="primary"
            @click="handleEdit(user)"
            >Edit</b-button
          >
          <b-button
            @click="handleDelete(user)"
            class="btn-danger"
            variant="danger"
            >Delete</b-button
          >
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'compt-list',
  students: {},
  props: {
    list: Array,
  },
  methods: {
    handleDelete(user) {
      //   console.log(user.id);
      this.$emit('deleteUser', user);
    },
    handleEdit(user) {
      this.$emit('editUser', user);
    },
  },
};
</script>

<style>
.table {
  border: 2px solid #000;
  width: 100%;
  margin-top: 20px;
}
.btn-danger {
  margin-left: 10px;
}
</style>
