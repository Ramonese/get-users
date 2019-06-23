<template>
  <form @submit.prevent="onSubmit">
    <div class="form-group">
      <div class="form-row">
        <div class="col md-auto">
          <label for="searchByPhoneNo" class="sr-only">search users</label>
          <input
            v-model="searchQuery"
            @keyup="validatePhoneNo"
            type="text"
            id="searchByPhoneNo"
            class="form-control form-control-sm"
            placeholder="Enter phone number"
          />
           <div :class="{isvalid: invalid-feedback}">
          Phone number must consist of + and 0-9
        </div>
        </div>
        <div class="col col-auto">
          <button type="submit" @click="validateForm" class="btn btn-primary btn-sm">Search</button>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
function isPhoneNo(input) {
  const regex = /[^+0-9]/g;
  return input.replace(regex, "");
}
//isPhoneNo("+33t  55hhhxx zz###") ;
export default {
  name: "SearchForm",
  props: ["search"],
  data: function() {
    return {
      searchQuery: "",
      isValid: false
    };
  },
  methods: {
    validatePhoneNo() {
      this.searchQuery = isPhoneNo(this.searchQuery);
    },
    validateForm() {
      //alert(this.searchQuery)
        this.searchQuery ? this.isValid = true : this.isValid = false;
      },
    onSubmit() {
      if(this.isValid) {
        alert("submit form")
        this.$emit("search", this.searchQuery);
        this.searchQuery = "";
        //this.isValid =false
      }
    }
  }
};
</script>
