<template>
  <div>
    <v-date-picker v-model="picker" elevation="2"></v-date-picker>
  </div>
</template>

<script>
export default {
  name: "Calendar",
  data() {
    return {
      picker: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
        .toISOString()
        .substr(0, 10),
    };
  },
};
</script>

<style scoped></style>
