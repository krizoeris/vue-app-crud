<template>
  <div id="app">
    <div class="container">
      <h1 class="mb-4 mt-4">Users</h1>
      <UserForm 
        @add:user="addUser" 
      />
      <UsersTable 
        v-bind:users='users' 
        @delete:user="deleteUser"
        @edit:user="editUser"
      />
    </div>
  </div>
</template>

<script>
import UsersTable from './components/UsersTable.vue'
import UserForm from './components/UserForm.vue'

export default {
  name: 'app',
  components: {
    UsersTable,
    UserForm
  },
  data() {
    return {
      users: [
        {
          id: 1,
          name: 'Kriztian Eris',
          email: 'kriztian.eris@gmail.com'
        },
        {
          id: 2,
          name: 'Juan Dela Cruz',
          email: 'juan@gmail.com'
        },
        {
          id: 3,
          name: 'John Doe',
          email: 'john@gmail.com'
        }
      ]
    }
  },

  methods: {
    addUser(user) {
      const lastId = this.users.length > 0 ? this.users[this.users.length - 1].id : 0;
      const id = lastId + 1;

      const newUser = {...user, id};

      this.users = [...this.users, newUser];
    },
    deleteUser(id) {
      this.users = this.users.filter(
        user => user.id !== id
      )
    },
    editUser(id, updatedUser) {
      this.users = this.users.map(user =>
        user.id === id ? updatedUser : user
      )
    }
  }
}
</script>

<style>
.container  {
  max-width: 700px;
}
</style>
