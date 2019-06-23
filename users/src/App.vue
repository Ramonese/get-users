<template>
  <div id="app">
    <div class="container bg-light pb-5 pt-3">
      <h1 class="border-bottom h2">Users</h1>
      <div v-if="loading">
        <div class="spinner-border text-primary" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div v-if="!loading">
        <SearchForm @search="searchByPhone"/>
        <div v-if="users.length">
          <UserList :users="users"/>
        </div>
        <div v-else>
          <Alert :message="errorText" />
        </div>  
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import _orderBy from "lodash";
import Alert from "./components/Alert.vue";
import SearchForm from "./components/SearchForm.vue";
import UserList from "./components/UserList.vue";
const getUsersUrl = "https://frontend-api-test.staging.netcore.lv/api/users";

export default {
  name: "app",
  components: {
    Alert, SearchForm, UserList
  },
  data: function() {
    return {
      users: [],
      loading: true,
      isError: false,
      errorText: 'No user found with this phone number'
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
          let data = response.data;
          this.users = _.orderBy(data, ['name']);
          this.loading = false;
        }
      } catch (error) {
        //TODO add error message
        this.errorText = 'No user found'
        this.isError = true;
        this.loading = false;
      }
    },
    async searchByPhone(input) {
      try {
        const response = await axios.get(
          `${getUsersUrl}/search?phone_number=${input}`
        );
        this.users = _.orderBy(response.data, ['name']);
      } catch (error) {
        this.errorText = 'No user found',
        this.isError = true;
      }
    },
  },
  computed: {}
};
</script>

