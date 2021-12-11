<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
p {
  color: red;
  text-align: center;
}
</style>
