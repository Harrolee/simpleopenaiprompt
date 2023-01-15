<script lang="ts">
export default {
  data() {
    return {
      text: "Edit me",
    };
  },
};
</script>

<template><input v-model="text" /> {{ text }}</template>
