<template>
    <div>
      <div class="card">
        <div class="card-body">
          <form @submit.prevent="submitUser">
            <div class="mb-3">
              <label for="name" class="form-label">Name:</label>
              <input v-model="newUser.name" type="text" class="form-control" id="name" placeholder="" required>
            </div>
            <div class="mb-3">
              <label for="email" class="form-label">Email:</label>
              <input v-model="newUser.email" type="email" class="form-control" id="email" placeholder="" required>
            </div>
            <button type="submit" class="btn btn-success me-2">Save</button>
            <button type="button" class="btn btn-primary" @click="updateUserFunction">Update</button>
          </form>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { mapState, mapActions } from 'vuex';
  
  export default {
    name: 'UserForm',
    data() {
      return {
        newUser: {
          name: '',
          email: ''
        },
        selectedUser: null
      };
    },
    computed: {
      ...mapState(['users'])
    },
    methods: {
      ...mapActions(['createUser', 'updateUser']),
      submitUser() {
        if (this.newUser.name && this.newUser.email) {
          this.newUser.name = this.newUser.name.toUpperCase();
          this.createUser(this.newUser);
          this.newUser = { name: '', email: '' };
        }
      },
      updateUserFunction() {
        if (this.selectedUser && this.newUser.name && this.newUser.email) {
          this.updateUser({ id: this.selectedUser.id, ...this.newUser });
          this.selectedUser = null;
          this.newUser = { name: '', email: '' };
        }
      }
    },
    watch: {
      selectedUser(newValue) {
        if (newValue) {
          this.newUser = { ...newValue };
        }
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  