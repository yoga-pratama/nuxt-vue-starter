<template>
  <v-container grid-list-xl fluid>
    <h4>
      <i class="fa fa-smile-o"></i>
      Hi there, this an empty page.
    </h4>

    <v-card ref="form">
      <v-card-text>
        <v-text-field
          label="Name"
          placeholder="John Doe"
          v-model="name"
          required
          ref="name"
          :rules="[() => !!name || 'Di isi woy']"
          :error-messages="errorMessages"
        ></v-text-field>
        <v-text-field
          label="Email"
          placeholder="John Doe"
          v-model="email"
          required
          ref="email"
          :rules="[() => !!email || 'Di isi woy']"
          :error-messages="errorMessages"
        ></v-text-field>
        <v-text-field
          label="Username"
          placeholder="John Doe"
          v-model="username"
          required
          ref="username"
          :rules="[() => !!username || 'Di isi woy']"
          :error-messages="errorMessages"
        ></v-text-field>
        <v-text-field
          label="password"
          placeholder="John Doe"
          v-model="password"
          required
          ref="password"
          :rules="[() => !!password || 'Isi Password']"
          :error-messages="errorMessages"
        ></v-text-field>

        <!-- <v-select
          autocomplete
          label="Country"
          placeholder="Select..."
          :rules="[() => !!negara || 'This field is required']"
          :items="countries"
          v-model="negara"
          ref="country"
          required
          multiple
        ></v-select> -->

        <v-btn color="primary" flat @click="simpan">Submit</v-btn>

        <!-- <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" flat @click="simpan" v-bind="attrs" v-on="on"
              >Submit</v-btn
            >
          </template>
          <span>Tooltip</span>
        </v-tooltip> -->
      </v-card-text>
    </v-card>

    <v-alert type="success"></v-alert>
  </v-container>
</template>

<script>
export default {
  layout: "dashboard",
  data() {
    return {
      name: "",
      username: "",
      email: "",
      password: "",
      errorMessages: [],
      negara: "",
      countries: ["Indonesia", "Malaysia"],
    };
  },
  methods: {
    simpan() {
      this.$axios
        .post("/addUser", {
          name: this.name,
          username: this.username,
          email: this.email,
          password: this.password,
        })
        .then((response) => {
          if (response.status == 201) {
            alert("Data tersimpan");
          }
        });
    },
  },
};
</script>

<style>
</style>