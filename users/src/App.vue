<template>
  <div id="app">
    <div class="container bg-light">
      <h1 class="border-bottom h3">Users</h1>
      
          
      <div v-if="loading">
      <div class="spinner-border text-primary" role="status">
        <span class="sr-only">Loading...</span>
      </div>
    </div>
    <div v-else>
      <form>
            <div class="form-group">
              <div class="row">
                <div class="col col-md-10 ">
                  <label for="search" class="sr-only">search users</label>
                  <input
                    v-model="searchQuery"
                    type="text"
                    class="form-control form-control-sm"
                    id="search"
                    aria-describedby="search user"
                    placeholder="Enter phone number"
                  >
                </div>
                <div class="col col-md-2">
                  <button
                    type="submit"
                    @click.prevent="getUser"
                    class="btn btn-primary btn-sm"
                  >Search</button>
                </div>
              </div>
            </div>
          </form>
       
      <UserList :users="users"/>
    </div>

    </div>

  </div>
</template>

<script>
import axios from "axios";
import UserList from "./components/UserList.vue";
const getUsersUrl = "https://frontend-api-test.staging.netcore.lv/api/users";

export default {
  name: "app",
  components: {
    UserList
  },
  data: function() {
    return {
      users: [],
       loading: true,
      searchQuery: "",
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
          (this.users = response.data), (this.loading = false);
        }
      } catch (error) {
        this.loading = false;
      }
    }
  },
  computed: {}
};
</script>

