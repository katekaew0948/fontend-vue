<template>
<v-row >
    <v-col cols="12">
  <Artist />
    </v-col>
</v-row>
</template>

<script>
export default {
    components: {
        Artist: () => import('../components/Artist.vue')
    }

}
</script>

<style>

</style>