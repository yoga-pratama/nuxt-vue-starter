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

    <v-flex lg12>
      <v-toolbar card color="white">
        <v-text-field
          flat
          solo
          prepend-icon="search"
          placeholder="Type something"
          v-model="search"
          hide-details
          class="hidden-sm-and-down"
        ></v-text-field>
        <v-btn icon>
          <v-icon>filter_list</v-icon>
        </v-btn>
      </v-toolbar>
      <v-data-table
        :headers="table_header"
        :items="users"
        :search="search"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td>{{ props.item.username }}</td>
          <td>{{ props.item.name }}</td>
          <td>{{ props.item.email }}</td>
          <td>{{ props.item.password }}</td>
          <td>
            <v-btn depressed outline icon fab dark color="primary" small @click="updateData(props.item)">
              <v-icon>edit</v-icon>
            </v-btn>
            <v-btn depressed outline icon fab dark color="pink" small @click="deleteData">
              <v-icon>delete</v-icon>
            </v-btn>
          </td>
        </template>
      </v-data-table>
    </v-flex>
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

      search: "",
      table_header: [
        {
          text: "Username",
          value: "username",
        },
        { text: "Name", value: "name" },
        { text: "Email", value: "email" },
        { text: "Password", value: "password" },
        { text: "Actions", value: "" },
      ],
      users: [],
    };
  },
  mounted() {
    this.getUserData();
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
    getUserData() {
      this.$axios.get("/getUser").then((response) => {
        // this.users = response.data.users;
        //console.log(this.users);
        response.data.users.forEach((el) => {
          console.log(el);
          var push_data = {
            name: el.name,
            username: el.username,
            email: el.email,
            password: el.password,
          };
          this.users.push(push_data);
        });

        console.log(this.users);
      });
    },
    updateData(item){
        alert(item.username);
    },
    deleteData(){
      alert('test');

    }
  },
};
</script>

<style>
</style>