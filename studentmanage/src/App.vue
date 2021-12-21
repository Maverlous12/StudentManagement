<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Header v-bind:title="title" />
    <Register :user="user" @save="clickAdd" @deleteAll="clickDeleteAll" />
    <ListTable
      v-bind:list="list"
      v-on:deleteUser="deleteUser"
      v-on:editUser="getUser"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import ListTable from './components/ListTable.vue';
import Register from './components/Register.vue';

export default {
  name: 'App',
  data() {
    return {
      user: {},
      title: 'Student Management',
      list: [
        {
          id: 1,
          name: 'Duong Anh Dung',
          age: 18,
          class: '1A',
          address: 'Ha Noi',
        },
        {
          id: 2,
          name: 'Le Ba Duong',
          age: 20,
          class: '3A',
          address: 'Nghe An',
        },
        {
          id: 3,
          name: 'Dao Cam Thanh',
          age: 23,
          class: '6B',
          address: 'Thanh Hoa',
        },
        {
          id: 4,
          name: 'Nguyen Huu Duc',
          age: 25,
          class: '8E',
          address: 'Ninh Binh',
        },
      ],
    };
  },
  components: {
    Header,
    ListTable,
    Register,
  },
  methods: {
    clickAdd(data) {
      // this.list.push(data);

      // console.log(data);
      // console.log(data);
      let index = this.list.findIndex((c) => c.id === data.id);
      if (index >= 0) {
        this.list.splice(index, 1, data);
      } else {
        // console.log('duong anh');
        let max = 0;
        let newID = 0;
        for (let i = 0; i < this.list.length; i++) {
          if (this.list[i].id > max) {
            max = this.list[i].id;
          }
        }
        newID = ++max;
        data.id = newID;
        this.list.push(data);
      }
      return;
    },
    deleteUser(a) {
      for (let i = 0; i < this.list.length; i++) {
        if (a.id === this.list[i].id) {
          this.list.splice(i, 1);
        }
      }
    },
    getUser(user) {
      this.user = user;
    },
    clickDeleteAll() {
      this.list.splice(0, this.list.length);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
