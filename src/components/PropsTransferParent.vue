<template>
  <PropsTransferChild :description="description" :type="type" :option="option"/>
</template>

<script>
import PropsTransferChild from "./PropsTransferChild";

export default {
  name: "PropsTransferParent",
  components: {
    PropsTransferChild,
  },
  props: ["option", "type", "description"],
};
</script>

<style lang="scss" scoped></style>
