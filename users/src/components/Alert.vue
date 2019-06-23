<template>
  <div class="alert alert-primary" role="alert">
    {{message}}
  </div>
</template>

<script>
export default {
  name: "Alert",
  props: ["message"]
};
</script>
