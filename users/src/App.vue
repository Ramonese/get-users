<template>
  <div id="app">
    <div class="container bg-light">
      <h1 class="border-bottom h2">Users</h1>

      <div v-if="loading">
        <div class="spinner-border text-primary" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div v-else>
        <SearchForm @search="searchByPhone"/>
        <div v-if="users.length">
          <UserList :users="users"/>
        </div>
        <div v-else>
          <p class="alert alert-primary" role="alert">No users found</p>
        </div>  
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import _orderBy from "lodash";
import SearchForm from "./components/SearchForm.vue";
import UserList from "./components/UserList.vue";
const getUsersUrl = "https://frontend-api-test.staging.netcore.lv/api/users";

export default {
  name: "app",
  components: {
    UserList, SearchForm
  },
  data: function() {
    return {
      users: [],
      loading: true,
      // errorIs:'',
      // errorText:'',
    };
  },
  mounted() {
    this.getUsers();
  },
  methods: {
    async getUsers() {
      try {
        const response = await axios.get(getUsersUrl);

        if (response.status === 200) {
          //TODO sort users by name
          let data = response.data;
          //console.log(data, typeof data )
          this.users = data;
          //  console.log( _orderBy(this.users, ['name'], ['asc']))
          //_orderBy(data, name);
          this.loading = false;
        }
      } catch (error) {
        //TODO add error message
        this.loading = false;
      }
    },
    async searchByPhone(input) {
      try {
        const response = await axios.get(
          `${getUsersUrl}/search?phone_number=${input}`
        );
          this.users = response.data;
      } catch (error) {
        console.log("User not found");
      }
    },
  },
  computed: {}
};
</script>

