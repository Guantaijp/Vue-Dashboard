<template>
  <div class="flex justify-between  mt-5">
    <div class="flex flex-col">
      <h1 class="text-2xl font-bold text-black">User Listing</h1>
      <p class="text-lg font-regular text-grey">User Listing</p>
    </div>
   <input
      type="text"
      class="h-10 bg-gray-100 px-3 pr-8 text-sm text-grey-darker border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
      placeholder="Search by name"
      v-model="searchText"
      @input="handleSearch"
    />
  </div>
  <div class="flex justify-between mt-5">
    <div class="flex mx-2 ">


      <select
        class="h-8 px-3 mx-3 pr-8 text-sm text-grey-darker bg-white border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
        v-model="accessType"
        @change="handleAccessChange"
      >
        <option value="">Select Access type</option>
        <option value="web">Web</option>
        <option value="mobile">Mobile</option>
        <option value="mobile & web">Web & Mobile</option>
      </select>


      <select
        class="h-8 mx-3 px-3 pr-8 text-sm text-grey-darker bg-white border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
        v-model="statusType"
        @change="handleStatusChange"
      >
        <option value="">Select Status</option>
        <option value="enabled">Enabled</option>
        <option value="disabled">Disabled</option>
      </select>


      <select
        class="h-8 mx-3 px-3 pr-8 text-sm text-grey-darker bg-white border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
        v-model="lableType"
        @change="handleLableChange"
      >
        <option value="">Select Label</option>
        <option value="admin">Admin</option>
        <option value="user">User</option>
        <option value="auditor">Auditor</option>
        <option value="sales">Sales Rep</option>
      </select>  
    </div>

   <div class="flex mx-5">
      <select
       class="h-8 mx-3 px-3 pr-8 text-sm text-grey-darker bg-white border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
       v-model="showHideOption" @change="handleShowHideOption">
       <option value="">Show / hide</option>
       <option value="show">Show all</option>
       <option value="hide">Hide all</option>
      </select>

      <select
         class="h-8 mx-3 px-3 pr-8 text-sm text-grey-darker bg-white border rounded outline-none mt-5 focus:outline-none focus:shadow-outline"
          v-model="dateSortOrder"
          @change="handleDateSort"
          >
          <option value="">Date Added</option>
          <option value="asc">Ascending</option>
          <option value="desc">Descending</option>
      </select>
    </div>
  </div>
</template>

<script>


export default {
  name: 'NavBar',
  props: {
    users: Array, // array of users
  },
  data() {
    return {
    searchText: '',
    accessType: '',
    statusType: '',
    lableType: '',
    showHideOption: '',
    dateOrder: '',
    };
  },
  methods: {
    handleSearch() {
      this.$emit('search', this.searchText,this.accessType,this.statusType, this.lableType);
    },
    handleAccessChange() {
      this.$emit('search', this.searchText, this.accessType,this.statusType, this.lableType);
    },
    handleStatusChange() {
      this.$emit('search', this.searchText, this.accessType, this.statusType, this.lableType);
    },
    handleLableChange() {
      this.$emit('search', this.searchText, this.accessType, this.statusType, this.lableType);
    },
    handleDateSort() {
      this.$emit('date-sort', this.dateSortOrder);
    },
    handleShowHideOption() {
      const newVisibilityState = this.showHideOption === 'hide';
      this.users.forEach(user => {
        user.detailsVisible = newVisibilityState;
      });
    },

  },
};
</script>

