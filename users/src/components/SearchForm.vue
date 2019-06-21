<template>
  <form>
    <div class="form-group">
      <div class="row">
        <div class="col col-md-10">
          <label for="searchByPhoneNo" class="sr-only">search users</label>
          <input
            v-model="searchQuery"
            type="text"
            id="searchByPhoneNo"
            class="form-control form-control-sm"
            placeholder="Enter phone number"
          >
        </div>
        <div class="col col-md-2">
          <button type="submit" @click.prevent="onSearch" class="btn btn-primary btn-sm">Search</button>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "SearchForm",
  props: ["search"],
  data: function() {
    return {
      searchQuery: ""
    };
  },
  methods: {
    onSearch() {
      this.$emit("search", this.searchQuery);
    }
  }
};
</script>
