<template>
  <form @submit.prevent="onSubmit">
    <div class="form-group">
      <div class="form-row">
        <div class="col md-auto">
          <label for="searchByPhoneNo" class="sr-only">phone number</label>
          <input
            v-model.trim="searchQuery"
            @keyup="validatePhoneNo"
            id="searchByPhoneNo"
            :class="{'is-invalid': !isValid}"
            type="text"
            autocomplete="false"
            class="form-control-sm form-control"
            placeholder="Enter phone number"
          />
          <div class="invalid-feedback">Phone number must start with + and consist of 0-9</div>
        </div>
        <div class="col col-auto">
          <button
            type="submit"
            class="btn btn-primary btn-sm"
            :class="{'disabled' : !isValid}">Search</button>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
function isPhoneNo(input) {
  //pattern: start with "+", then at least 1 number
  const regex = /[+][0-9][0-9]*$/;
  return input.match(regex) ? true : false;
}
export default {
  name: "SearchForm",
  props: ["search"],
  data: function() {
    return {
      searchQuery: "",
      isValid: true
    };
  },
  methods: {
    validatePhoneNo() {
      let status = isPhoneNo(this.searchQuery);
      //allow epmty form submission to retrieve all numbers from DB
      if (status || !this.searchQuery) {
        this.isValid = true
      }
      else {
        this.isValid = false;
      }
    },
    onSubmit() {
      if (this.isValid) {
        this.$emit("search", this.searchQuery);
        this.searchQuery = "";
        this.isValid = true;
      }
    }
  }
};
</script>
