<template>
  <div id="app" class="container mt-5">
    <div class="row">
      <div class="col-md-6">
        <UserForm @userSelected="selectedUser = $event" />
      </div>
      
      <div class="col-md-6">
        <UserList @userSelected="selectedUser = $event" />
      </div>
    </div>
  </div>
</template>

<script>
import UserForm from './components/UserForm.vue';
import UserList from './components/UserList.vue';

export default {
  name: 'App',
  components: {
    UserForm,
    UserList
  },
  data() {
    return {
      selectedUser: null
    };
  }
};
</script>

<style>
</style>
