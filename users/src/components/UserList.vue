<template>
  <div class="accordion">
    <UserListItem v-for="user in users" :key="user.id" :user="user" />
  </div>
</template>

<script>
import UserListItem from "./UserListItem";

export default {
  name: "UserList",
  components: {
    UserListItem
  },
  props: ["users"]
};
</script>
