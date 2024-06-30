<template>
    <div>
      <div class="card">
        <div class="card-body ">
          <h5 class="card-title">List of Users</h5>
          <div v-if="users.length === 0" class="text-muted">
            - no user created -
          </div>
          <div v-else>
            <div v-for="user in users" :key="user.id" class="mb-2 p-2 border rounded bg-info bg-gradient">
              <div>{{ user.name }}</div>
              <div class="text-muted">{{ user.email }}</div>
              <div class="mt-2">
                <button @click="chooseUser(user)" class="btn btn-primary btn-sm me-2">Choose</button>
                <button @click="removeUser(user.id)" class="btn btn-danger btn-sm">Remove</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { mapState, mapActions } from 'vuex';
  
  export default {
    name: 'UserList',
    computed: {
      ...mapState(['users'])
    },
    methods: {
      ...mapActions(['fetchUsers', 'deleteUser']),
      chooseUser(user) {
        this.$emit('userSelected', user);
      },
      removeUser(userId) {
        if (window.confirm('Are you sure you want to remove this user?')) {
          this.deleteUser(userId);
        }
      }
    },
    mounted() {
      this.fetchUsers();
    }
  };
  </script>
  
  <style scoped>
  </style>
  