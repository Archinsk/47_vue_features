<template>
  <div class="row">
    <div class="col">{{ description }}</div>
    <div class="col">{{ type }}</div>
    <div class="col">{{ option }}</div>
  </div>
</template>

<script>
export default {
  name: "PropsTransferChild",
  props: ["option", "type", "description"],
};
</script>

<style lang="scss" scoped></style>
