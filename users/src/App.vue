<template>
  <div id="app">
    <div class="container bg-light">
       <h1 class="border-bottom h3">Users</h1>
      <div class="row">
       
        <div class="col">
          <form>

            <div class="form-group">
              <div class="row">
                <div class="col col-md-auto">
                  <label for="search" class="sr-only">search users</label>
                  <input
                    type="text"
                    class="form-control form-control-sm"
                    id="search"
                    aria-describedby="search user"
                    placeholder="Enter phone number"
                  >
                </div>
                <div class="col col-lg-1">
                  <button type="submit" class="btn btn-primary btn-sm">Search</button>
                </div>
            </div>
            </div>
          </form>
        </div>
      </div>
    </div>
    
    <!-- <Users/> -->
  </div>
</template>

<script>
import Users from "./components/Users.vue";

export default {
  name: "app",
  components: {
    Users
  }
};
</script>

<style>
</style>
