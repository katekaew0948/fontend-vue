<template>
  <v-form v-model="valid" light>
    <v-container fluid>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            :counter="10"
            label="Content"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="lastname"
            :rules="nameRules"
            :counter="10"
            label="Pen Name"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="12" md="4">
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="Rate price"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="Contact"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-file-input accept="image/*" label="File input"></v-file-input>
        </v-col>
      </v-row>
      <v-col cols="12">
        <v-textarea
          background-color="grey lighten-2"
          color="cyan"
          label="Detail"
        ></v-textarea>
      </v-col>
      <v-row> </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    firstname: "",
    lastname: "",
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => v.length <= 10 || "Name must be less than 10 characters",
    ],
    email: "",
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+/.test(v) || "E-mail must be valid",
    ],
  }),
};
</script>

<style>
.fill-height {
  background-image: url("../assets/starry_sky.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>