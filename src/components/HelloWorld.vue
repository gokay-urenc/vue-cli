<template>
  <div>
    <h4 class="alert alert-success">{{ msg }}</h4>
    <h4 class="alert alert-danger">{{ nmbr }}</h4>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    nmbr: Number
  }
};
</script>

<style scoped>
</style>