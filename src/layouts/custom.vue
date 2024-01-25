<script lang="ts" setup>
import CustomLayoutWithVerticalNav from "@/layouts/components/CustomLayoutWithVerticalNav.vue";
</script>

<template>
  <CustomLayoutWithVerticalNav>
    <RouterView />
  </CustomLayoutWithVerticalNav>
</template>

<style lang="scss">
// As we are using `layouts` plugin we need its styles to be imported
@use "@layouts/styles/default-layout";
</style>
