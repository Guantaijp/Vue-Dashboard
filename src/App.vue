<template>
  <div id="app">
    <NavBar 
    :users="users" 
    @search="handleSearch"
    @toggle-details="toggleUserDetails" 
    @date-sort="handleDateSort"
    />
    <DatatablePage 
    :users="filteredUsers" 
    @delete-user="deleteUser" 
    @edit-user="editUser" 
    @toggle-details="toggleUserDetails" />
   </div>
</template>


<script>
import NavBar from './components/NavBar.vue';
import DatatablePage from './components/DatatablePage.vue';
import { users } from './components/userData.js:';

export default {
  name: 'App',
  components: {
    NavBar,
    DatatablePage,
  },
  data() {
    return {
      users: users.map(user => ({ ...user, detailsVisible: false })),
      searchText: '', 
      accessType: '',
      statusType: '',
      lableType: '',
      dateOrder: '',
     
    };
  },
  computed: {
    filteredUsers() {
      let filteredUsers = this.users;
      if (this.searchText) { // Change this from searchUsername to searchText
        const searchLower = this.searchText.toLowerCase();
        filteredUsers = filteredUsers.filter(
          user => user.username.toLowerCase().includes(searchLower)
        );
      }

      if (this.accessType) {
        filteredUsers = filteredUsers.filter(user => user.access === this.accessType);
      }

      if (this.lableType) {
        filteredUsers = filteredUsers.filter(user => user.lable === this.lableType);
      }

      if (this.statusType) {
        filteredUsers = filteredUsers.filter(user => user.status === this.statusType);
      }

      if (this.hideType) {
        filteredUsers = filteredUsers.filter(user => user.hide === this.hideType);
      }
      return filteredUsers;
    },
  },
  methods: {
    //search user
    handleSearch(searchText, accessType, statusType, lableType, hideType, dateOrder) {
      this.searchText = searchText;
      this.accessType = accessType;
      this.statusType = statusType;
      this.lableType = lableType;
      this.hideType = hideType;
      this.dateOrder = dateOrder;
    },

    //delete user
    deleteUser(userToDelete) {
    // Find the index of the user to delete in the users array
    const indexToDelete = this.users.findIndex(user => user.id === userToDelete.id);

    if (indexToDelete !== -1) {
      // Remove the user from the users array
      this.users.splice(indexToDelete, 1);
    }
  },
  //edit user
  editUser(userToEdit) {
    // Find the index of the user to edit in the users array
    const indexToEdit = this.users.findIndex(user => user.id === userToEdit.id);

    if (indexToEdit !== -1) {
      // Replace the user in the users array with the edited user
      this.users.splice(indexToEdit, 1, userToEdit);
    }
  },
  //view user details or hide user details
    toggleUserDetails(userToToggle) {
      const indexToToggle = this.users.findIndex(user => user.id === userToToggle.id);

      if (indexToToggle !== -1) {
        this.users[indexToToggle].detailsVisible = !this.users[indexToToggle].detailsVisible;
      }
    },
      handleDateSort(sortOrder) {
      if (sortOrder === 'asc') {
        this.users.sort((a, b) => new Date(a.date) - new Date(b.date));
      } else if (sortOrder === 'desc') {
        this.users.sort((a, b) => new Date(b.date) - new Date(a.date));
      }
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  margin: 30px;
}
</style>

