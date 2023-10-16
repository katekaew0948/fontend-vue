<template>
  <v-row>
    <v-col cols="12">
      <Content />
    </v-col>
  </v-row>
</template>

<script>
export default {
  components: {
    Content: () => import("../components/Content.vue"),
  },
};
</script>

<style>
</style>